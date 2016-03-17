---
author: srt
comments: true
date: 2008-05-10 20:05:38+00:00
excerpt: '<p>

  A few weeks ago, Matt Gibson <a href="http://lists.digium.com/pipermail/asterisk-users/2008-April/209914.html">posted
  on the asterisk-users discussion list</a> that he was looking for a GraphViz script
  he had heard about a few years ago that could generate graphs of Asterisk''s <tt>extensions.conf</tt>
  file that defines the dialplan. At the time, I had been working on a <a href="http://www.sourceforge.net/projects/egonet/">recently
  open-sourced application, EgoNet</a>, for a researcher I work with. This application
  taught me much about social networks, particularly his specialty of egocentric networks,
  and it also helped me learn a ton about the <a href="http://jung.sourceforge.net/">Java
  Universal Network/Graph Framework (or JUNG)</a>. I immediately thought about combining
  my experience with JUNG and Asterisk, and wrote a rudimentary (read as: extremely
  ugly) parser for extensions.conf and generated a crude graph of the sample dialplan.

  </p>'
layout: post
permalink: visualizing-your-dialplan-with-a-graph-456
slug: visualizing-your-dialplan-with-a-graph
title: Visualizing your dialplan with a graph
wordpress_id: 456
tags:
- asterisk-java
- dialplan
- jung
- visualization
---


A few weeks ago, Matt Gibson [posted on the asterisk-users discussion list](http://lists.digium.com/pipermail/asterisk-users/2008-April/209914.html) that he was looking for a GraphViz script he had heard about a few years ago that could generate graphs of Asterisk's extensions.conf file that defines the dialplan. At the time, I had been working on a [recently open-sourced application, EgoNet](http://egonet.sf.net/), for a researcher I work with. This application taught me much about social networks, particularly his specialty of egocentric networks, and it also helped me learn a ton about the [Java Universal Network/Graph Framework (or JUNG)](http://jung.sourceforge.net/). I immediately thought about combining my experience with JUNG and Asterisk, and wrote a rudimentary (read as: extremely ugly) parser for extensions.conf and generated a crude graph of the sample dialplan.






Here's a picture of it:






![Original Dialplan Visualization](https://blogs.reucon.com/asterisk-java/files/2011/12/original-extensions-conf-sample.jpg)








I posted my image back to the list and got many interesting responses. Given all of the interest, and remembering that Stefan had [recently added some config file parsing to Asterisk-Java](http://sourceforge.net/mailarchive/forum.php?thread_name=47CEBE09.7030405%40reucon.com&forum_name=asterisk-java-devel) for management of the configuration file format Asterisk uses, I decided to add extensions.conf-specific parsing to his original work.







So far, I've only written in some very, very simple grouping of the different kinds extensions.conf statements, specifically support for _exten_ and _include_. I've also added the parsing of the exten line to recognize the extension name, priority, application, and arguments. Because the authoritative source for all of this is pbx_config.c, I couldn't resort to flex or bison. At the moment, I haven't differentiated any further into interpreting the dialplan, as I don't really care about things like priorities like _same_ or _n+1_ or anything other than basic structure.









Without further ado, I'd like to show some of what can be done with the dialplan specific parsing I've done, and give some examples, including a Java Web Start demo (so get your extensions.conf file ready!).







**Example 0: Just printing out the parsed information**  


Initially, I just wanted a trivial example to print out what I had parsed. Here, I print out every context and its extensions. Below is the code, and then the output. I trimmed the output to show what new classes I've created outside of Stefan's original config package. The important ones are ConfigInclude and ConfigExtension, as those will give us some ties for our graph.






Code for Example 0:



    
    
    public class GraphExample0
    {
        public static void main(String [] args) throws Exception
        {
            ExtensionsConfigFile configFile = readFile();
            for(Category ctx : configFile.getContexts())
            {
                System.out.println(ctx.getClass().getSimpleName() + ": " + ctx + " (base " + ctx.getBaseCategories() + ") --");
                for(ConfigElement el : ctx.getElements())
                    System.out.println("\t" + el.getClass().getSimpleName() + ": "+ el);
            }
        }
        
        public static ExtensionsConfigFile readFile() throws Exception
        {
            String fileName = "./extensions.conf.bebr";
            ExtensionsConfigFileReader fileReader = new ExtensionsConfigFileReader();
            ExtensionsConfigFile configFile = fileReader.readExtensionsFile(fileName);
            return configFile;
        }
    }
    





Output for Example 0:



    
    
    Category: general (base []) --
    	ConfigVariable: static=yes
    	ConfigVariable: writeprotect=no
    	ConfigVariable: clearglobalvars=no
    Category: macro-dundi-e164 (base []) --
    	ConfigExtension: exten => s,1,[Goto, ${ARG1}, 1]
    	ConfigInclude: include => dundi-e164-lookup
    






**Examples 1 & 2: Initial network graph definition**
  

The next step was to decide what to graph. Because contexts are the major structural feature in a dialplan, I chose to make contexts the nodes. Next, I needed to decide what ties contexts together in order to have some edges in my graph. I chose include statements so that my graph would show the overall structure of the dialplan. You could choose anything for the ties, and later on, I throw in Goto statements as well. As you can see from the code examples, I had to add two new methods -- one for figuring out the nodes (buildGraph) and one for figuring the edges around that node (getIncludesContext). After looking at the output, I decided I needed labels on my nodes and edges. That's example 2, which I haven't shown in code here (it's included in the download at the end of the article). Finally, for example 2, I created a class, SimpleGraphViewer that handled the graph part of things here. It is based directly from the ShowLayouts demo in JUNG.





    
    
        public static void main(String[] args) throws Exception
        {
            ExtensionsConfigFile configFile = readFile();
            Graph<Category, ConfigInclude> graph = buildGraph(configFile);
            
            Layout<Category, ConfigInclude> layout = new KKLayout<Category, ConfigInclude>(graph);
            VisualizationViewer<Category, ConfigInclude> vv = new VisualizationViewer<Category, ConfigInclude>(layout);
            
            JPanel jp = new JPanel();
            jp.setBackground(Color.WHITE);
            jp.setLayout(new BorderLayout());
            jp.add(vv, BorderLayout.CENTER);
    
            JFrame frame = new JFrame();
            frame.add(vv);
            frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            frame.pack();
            frame.setVisible(true);
        }
        
        static Graph<Category, ConfigInclude> buildGraph(ExtensionsConfigFile configFile)
        {
            Graph<Category, ConfigInclude> graph = new DirectedSparseGraph<Category, ConfigInclude>();
            for (Category c1 : configFile.getContexts())
            {
                for (Map.Entry<ConfigInclude,Category> entry : getIncludesContext(c1, configFile.getContexts()).entrySet())
                {
                    Category c2 = entry.getValue();
                    System.out.println("adding " + entry.getKey());
                    graph.addEdge(entry.getKey(), c1, c2, EdgeType.DIRECTED);
                }
            }
            return graph;
        }
        
        /**
         * Given an unchanging list of all possible config categories, and an origin
         * category, find the list of all destination categories; a destination is
         * defined as an include statement for this example.
         * 
         * @param originatingContext the context for which you want to find destinations
         * @param fullList the full list of contexts, after parsing has completed
         * @return all destination contexts mapped by the config directive that references them
         */
        public static Map<ConfigInclude,Category> getIncludesContext(Category originatingContext, Collection<Category> fullList)
        {
            Map<ConfigInclude,Category> dest = new HashMap<ConfigInclude,Category>();
            for(ConfigElement e : originatingContext.getElements())
            {
                if(!(e instanceof ConfigInclude))
                    continue;
                
                ConfigInclude searchingContext = ((ConfigInclude)e);
                for(Category candidateContext : fullList)
                {
                    if(originatingContext == candidateContext)
                        continue;
                    
                    if(!searchingContext.getName().trim().toLowerCase().equals(candidateContext.getName().trim().toLowerCase()))
                            continue;
                    
                    dest.put(searchingContext, candidateContext);
                }
            }
            return dest;
        }
    






Here's the output graphs of examples 1 and 2:
  

[![Example 1](https://blogs.reucon.com/asterisk-java/files/2011/12/viz-example1.jpg)](https://blogs.reucon.com/asterisk-java/files/2011/12/viz-example1.jpg)

[![Example 2](https://blogs.reucon.com/asterisk-java/files/2011/12/viz-example2.jpg)](https://blogs.reucon.com/asterisk-java/files/2011/12/viz-example2.jpg)







**Example 3: Adding even more to the graph**  

After I saw example 2, I wanted to add Goto() statements as green edge ties to other context nodes and I wanted to size nodes by how many extensions they had. I also wanted to clean up all of the labeling by using color. I used JUNG's normal ways of doing both of these, which you may follow along with in the code samples. These graphs are starting to look really neat.





    
    
        // change this to xyzzy to keep macros in the graph
        static final String ignorePrefix = "macro-";
        
        static Graph<Category, ConfigElement> buildGraph2(ExtensionsConfigFile configFile)
        {
            Graph<Category, ConfigElement> graph = new DirectedSparseMultigraph<Category, ConfigElement>();
            for (Category c1 : configFile.getContexts())
            {
                if(c1.getName().toLowerCase().startsWith(ignorePrefix))
                    continue;
    
                for (Map.Entry<ConfigInclude,Category> entry : getIncludesContext(c1, configFile.getContexts()).entrySet())
                {
                    Category c2 = entry.getValue();
                    if(c2.getName().toLowerCase().startsWith(ignorePrefix))
                        continue;
                    
                    if(!graph.containsEdge(entry.getKey()))
                    {
                        System.out.println("adding " + entry.getKey());
                        graph.addEdge(entry.getKey(), c1, c2, EdgeType.DIRECTED);
                    }
                }
                for (Map.Entry<ConfigExtension,Category> entry : getGotoContext(c1, configFile.getContexts()).entrySet())
                {
                    Category c2 = entry.getValue();
                    if(c2.getName().toLowerCase().startsWith(ignorePrefix))
                        continue;
                    
                    if(!graph.containsEdge(entry.getKey()))
                    {
                        System.out.println("adding " + entry.getKey());
                        graph.addEdge(entry.getKey(), c1, c2, EdgeType.DIRECTED);
                    }
                }
            }
            return graph;
        }
        
        public static Map<ConfigExtension,Category> getGotoContext(Category originatingContext, Collection<Category> fullList)
        {
            Map<ConfigExtension,Category> dest = new HashMap<ConfigExtension,Category>();
            for(ConfigElement e : originatingContext.getElements())
            {
                if(!(e instanceof ConfigExtension))
                    continue;
                
                ConfigExtension searchingContext = ((ConfigExtension)e);
                String [] app = searchingContext.getApplication();
                
                // skip everything but goto and gotoif
                if(!(app.length == 4 && app[0].toLowerCase().startsWith("goto")))
                    continue;
    
                String searchingContextString = app[1];
                
                for(Category candidateContext : fullList)
                {
                    if(originatingContext == candidateContext)
                        continue;
                    
                    if(!searchingContextString.trim().toLowerCase().equals(candidateContext.getName().trim().toLowerCase()))
                            continue;
                    
                    dest.put(searchingContext, candidateContext);
                }
            }
            return dest;
        }
    
        public static void main(String[] args) throws Exception
        {
            ExtensionsConfigFile configFile = readFile();
            Graph<Category,ConfigElement> graph = buildGraph2(configFile);
            
            Layout<Category,ConfigElement> layout = new KKLayout<Category, ConfigElement>(graph);
            VisualizationViewer<Category, ConfigElement> vv = new VisualizationViewer<Category, ConfigElement>(layout);
            
            vv.getRenderContext().setVertexLabelTransformer(new CategoryNameLabeller());
            vv.getRenderContext().setVertexShapeTransformer(new CategorySizeAspect());
            vv.getRenderContext().setEdgeDrawPaintTransformer(new EdgePaintSelector(vv));
    
            new SimpleGraphViewer<Category, ConfigElement>(vv).setVisible(true);
        }
        
        public static class CategorySizeAspect 
        extends AbstractVertexShapeTransformer<Category>
        implements Transformer<Category,Shape>
        {
            int maxEdges = 0;
            
            public CategorySizeAspect()
            {
                super();
                setSizeTransformer(new Transformer<Category,Integer>() {
                    public Integer transform(Category v) {
                            return (int)(v.getElements().size()) + 25;
                    }});
            }
    
            @Override
            public Shape transform(Category cat)
            {
                return factory.getEllipse(cat);
            }
        }
    
        public static class EdgePaintSelector
        implements Transformer<ConfigElement,Paint>
        {
            GradientEdgePaintTransformer<Category,ConfigElement> includesEdge;
            GradientEdgePaintTransformer<Category,ConfigElement> gotoEdge;
            GradientEdgePaintTransformer<Category,ConfigElement> unknownEdge;
    
            public EdgePaintSelector(VisualizationViewer<Category,ConfigElement> vv)
            {
                includesEdge = new GradientEdgePaintTransformer<Category,ConfigElement>(Color.blue.darker().darker(),Color.blue,vv);
                gotoEdge = new GradientEdgePaintTransformer<Category,ConfigElement>(Color.green.darker().darker(),Color.green,vv);
                unknownEdge = new GradientEdgePaintTransformer<Category,ConfigElement>(Color.white,Color.white,vv);
            }
            
            @Override
            public Paint transform(ConfigElement e)
            {
                if(e instanceof ConfigInclude)
                    return includesEdge.transform(e);
                else if(e instanceof ConfigExtension)
                    return gotoEdge.transform(e);
                return unknownEdge.transform(e);
            }
            
        }
    
        public static ExtensionsConfigFile readFile2() throws Exception
        {
            JFileChooser jfc = new JFileChooser();
            int result = jfc.showOpenDialog(null);
            if(result != JFileChooser.APPROVE_OPTION)
                return new ExtensionsConfigFile("",new HashMap<String,Category>());
            
            File file = jfc.getSelectedFile();
            String fileName = file.getPath();
            
            ExtensionsConfigFileReader fileReader = new ExtensionsConfigFileReader();
            ExtensionsConfigFile configFile = fileReader.readExtensionsFile(fileName);
            return configFile;
        }
    






Here's the output of the extensions.conf that comes default with Asterisk, as well as output from a more complex dialplan I picked up along the way.  

[![Example 3](https://blogs.reucon.com/asterisk-java/files/2011/12/viz-example3.jpg)](https://blogs.reucon.com/asterisk-java/files/2011/12/viz-example3.jpg)

[![Example 3b](https://blogs.reucon.com/asterisk-java/files/2011/12/viz-example3b.jpg)](https://blogs.reucon.com/asterisk-java/files/2011/12/viz-example3b.jpg)







**Try it on your own extensions.conf**  

[![[Launch to try the demo]](https://blogs.reucon.com/asterisk-java/files/2011/12/webstart-demobutton.png)](https://blogs.reucon.com/asterisk-java/files/2011/12/asterisk-java-jung-visualization-demo.jnlp) or skip ahead to [download the JAR file](https://blogs.reucon.com/asterisk-java/files/2011/12/asterisk-java-jung-visualization-demo.jar) containing the source (see the org.mbs3.* packages for the demo sources, the rest of the JAR is JUNG and Asterisk-Java).







**Please note:** The web start demo requires you to accept a self-signed certificate as web start won't allow the demo to read the local extensions.conf file you select! If you're worried about this, feel free to download and build the source yourself.







Here's what the demo looks like with my extensions.conf and JUNG's [ISOMLayout](http://jung.sourceforge.net/doc/api/edu/uci/ics/jung/visualization/ISOMLayout.html). The demo contains two different mouse modes for interacting with the graph as well as a button to save the image. If the demo doesn't work, or you encounter any trouble or things that need to be corrected, feel free to reply and let me know. Thanks!







[![Example 3c](https://blogs.reucon.com/asterisk-java/files/2011/12/viz-example3c.jpg)](https://blogs.reucon.com/asterisk-java/files/2011/12/viz-example3c.jpg)





