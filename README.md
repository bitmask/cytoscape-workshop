# CBioVikings Workshop -- Introduction to biological networks in Cytoscape

This exercise is designed for Cytoscape 3.3.0, and should work with earlier versions (with slight modifications to the import instructions). 

Citation: Shannon, P., Markiel, A., Ozier, O., Baliga, N. S., Wang, J. T., Ramage, D., … Ideker, T. (2003). Cytoscape: a software environment for integrated models of biomolecular interaction networks. Genome Res, 13(Karp 2001), 2498–2504. doi:10.1101/gr.1239303 http://genome.cshlp.org/content/13/11/2498.full

We are going to take a list of proteins that are associated with diabetes, and create a network with them, which we will investigate in cytoscape. We will overlay pancreas expression data onto the network, and make some observations about the proteins and processes involved in diabetes.  The network will come from STRING, so we will first download this data. 

The following exercises contain some questions for you to answer,
> and the answers are formatted like this.

## 0.1. Query STRING for a single protein

STRING is a database of known and predicted protein interactions. The interactions include direct (physical) and indirect (functional) associations; they are derived from four sources: Genomic Context, High-throughput Experiments, (Conserved) Coexpression and Previous Knowledge.  STRING quantitatively integrates interaction data from these sources for a large number of organisms, and transfers information between these organisms where applicable. The database currently covers 9,643,763 proteins from 2,031 organisms.

Go to http://string-db.org/ and query for human insulin receptor (INSR) using the search by name functionality. This will return a network of interaction partners for the insulin receptor in human.  Nodes are connected by different types of evidence, which you can investigate further down on the page.  

Citation: Szklarczyk, D., Franceschini, A., Wyder, S., Forslund, K., Heller, D., Huerta-Cepas, J., … Von Mering, C. (2015). STRING v10: Protein-protein interaction networks, integrated over the tree of life. Nucleic Acids Research, 43(D1), D447–D452. doi:10.1093/nar/gku1003 https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4383874/

## 0.2. Query STRING for multiple proteins

In addition to providing interaction partners for a protein of interest, STRING is also commonly used to obtain a network for a set of proteins of interest. In this question, we will generate a diabetes protein network, which will also be used in the subsequent Cytoscape exercise. To this end we provide you with this file: diabetes.txt, which contains 287 proteins associated with diabetes mellitus according to the DISEASES database (http://diseases.jensenlab.org).

Citation: Pletscher-Frankild, S., Pallej??, A., Tsafou, K., Binder, J. X., & Jensen, L. J. (2015). DISEASES: Text mining and data integration of disease-gene associations. Methods, 74, 83–89. doi:10.1016/j.ymeth.2014.11.020 http://www.sciencedirect.com/science/article/pii/S1046202314003831

Return to the front page of STRING and go to the multiple names tab. Either paste in the list of identifiers of diabetes proteins, or upload the file via the web interface. To speed up the query for this many proteins, you may want to specify that these are human proteins instead of relying on the species to be automatically detected.

The network obtained with default parameters contains a large central component with very high connectivity (colloquially referred to as a “hairball”). This is primarily because many of the proteins have been studied extensively, in part due to their role in diabetes. To produce a less highly connected network, restrict it to consider only high confidence (0.700) interactions.

The network contains some proteins with no interactions (singletons). Why do you see singletons when querying for multiple proteins and not when querying for only one protein?

> When querying for multiple proteins, you see all the proteins you queried for and only the interactions among them; there
> can thus easy be some proteins in the set that interacts with nothing else in the set. When querying for only a single
> protein, the additional proteins are retrieved based on the fact that they interact with the query protein; they thus by 
> definition have at least one interaction partner.

You can remove the singletons from the visualization by turning on advanced mode in the network viewer and selecting Hide disconnected nodes from the Options menu.

To work with the network in Cytoscape in the next exercise, you need to save it to a file. From the Save menu, select Other formats, then choose the first non-image format in the list, which is called Text Summary.

If you have time, feel free to explore the other functions of the advanced mode or to query STRING for your own proteins of interest.

## 1. Import the network into Cytoscape

Open Cytoscape, start a new session from a network file.  Import -> Network -> From File.  In the import dialog, the first column will be the 'Source node' (green circle), the second column will be the 'Target node' (red target).  The rightmost column 'Combined score' will be and edge attribute (blue page), and all the other columns do not need to be imported.  

## 2. Visualize the network

Cytoscape provides several visualization options under the Layout menu.  Experiment with these and find one that allows you to see the shape of the network easily.

> Layout -> Edge-weighted spring embedded -> combined score 
> This works pretty well to see the network structure, other layouts are also reasonable.

## 3. Inspect tissue expression data

We are going to overlay information about which tissues the proteins are expressed in onto the network.  This data comes from the Tissues database, which we will take a look at first to better understand the data.

Go to http://tissues.jensenlab.org/ and enter insulin (gene name: INS) into the search box.  The resulting page will show you an overall representation of where in the body insulin is located, and below you can see tables containing the specific lines of evidence that contribute to the overall score.  

Citation: Santos, A., Tsafou, K., Stolte, C., Pletscher-Frankild, S., O’Donoghue, S. I., & Jensen, L. J. (2015). Comprehensive comparison of large-scale tissue expression datasets. PeerJ, 3, e1054. doi:10.7717/peerj.1054 https://peerj.com/articles/1054/

What tissues is insulin present in with a confidence of 4 or above?  What source do these interactions come from?

> Pancreas and blood.  They come from the knowledge channel and are derived from the human insulin Uniprot entry. 

## 4. Add pancreas data to the network

We'll now add the expression data to the network.  We have already generated a file for you to use that has been filtered for expression in the pancreas.  Download it here: pancreas_proteins.txt.

Load it into Cytoscape with File -> Import -> Table -> File

We are importing tissue expression data which indicates whether a protein is expressed in the pancreas or not, so this means the data is about the nodes -- make sure that 'Import Data As' is set to 'Node Table Columns'.  You should see the column headers in the first line of the preview pane, and gene_name will be the key (key icon) and confidence will be an attribute (page icon).  The new columns will be added to the table in the bottom panel, and they will be available for styling. 

## 5. Style the network

Cytoscape allows you to map properties of the nodes and edges (like those we have just imported) to visual parameters such as node colour and edge width.  We will map the pancreas expression data to the node colour.

From the left panel top menu, select 'Style' (it's to the right of 'Network').  Then click on the triangle to the right of the property you want to change, for example node fill color.  Note here that you can also change the styling of edge properties by clicking on Edge at the bottom of the panel.

Next, set the 'Mapping Type' to the column containing the data that you want to use (confidence).  Although this is a numeric value, there are only two distinct values, so we will use the 'Discrete Mapping', and set a different color for each value.  Click on the square to the right of the value, then click on ... and select an appropriate colour.  

Many proteins will not be associated with the pancreas -- they will retain the default styling (which you are free to change in the same manner by clicking on the default value in the far left of the Fill Colour line.  

## 6. Use clusterMaker to find clusters 

clusterMaker is a Cytoscape App, which we will first need to install.  Go to Apps -> App Manager and type clusterMaker2 into the search box.  Select it from the middle pane, and click install.  You will need to be connected to the internet for this step to work.  When this is done close the App Manager, and you will be able to find clusterMaker under the Apps menu.

Select it now, and choose the MCODE clustering algorithm.  When it is done, it will have added another column to each node containing the number of the cluster the node has been assigned to.  To actually visualize the network, go to Apps -> clusterMaker Visualizations -> Create network from clusters.

How many clusters are generated?  (Don't count nodes with degree 0.) 

> There are 5 clusters.

Look at the cluster containing INSR.  Which are the three proteins in this cluster that are related to the pancreas?  Look up the functions of the three proteins if you don't know them.  

> ABCC8 -- ABC transporter, modulator of insulin release
> GCK -- Glucokinase, first step in glucose metabolism
> GCG -- Glucagon, regulates blood glucose by increasing gluconeogenesis and decreasing glycolysis.


## 7. Use BINGO to do an enrichment analysis

Now we will use another Cytoscape app, BINGO, to investigate the Gene Ontology terms associated with the proteins in our subnetwork.

Install BINGO the same way you installed clusterMaker.  Then, we will run BINGO just on the subnetwork we looked at in question 6, so select these nodes, then go to Apps -> BINGO.  Give a name to the cluster, for example "INSR cluster", and then make sure you select Human in the organism drop down.  The other parameters are correct -- we want to use a hypergeometric test, and correct for multiple testing.  

This will generate a new network and a table, both of which contain information about the GO terms that are associated with the proteins in our network. 

What is the GO term with the lowest p-value?  If there is a tie, take the more specific GO term.

> glucose homeostasis; p-value = 6.9e-13

Explore the network of GO terms and understand how the colour of the nodes represents the p-value, and what the directionality of the edges in the network means, and how the most significant nodes are distributed in the network. 

> More orange nodes have more significant p-values.  The target of an edge is more specific GO term than the source (source -> target).  The most significant GO terms are those that are most specific -- at the ends of long paths and away from hubs.  


## 8. Run the network analyzer on the protein network

We will now go back to the original network, and analyze it.  Run the network analyzer under Tools -> Network Analyzer -> Network Analysis -> Analyze Network.  Should the network be treated as directed or undirected?  Remember the network comes from STRING.

Should be treated as undirected, since STRING records that proteins are functionally related, but does not store a direction of this interaction. 

Examine the Node Degree Distribution panel in the Results Panel.  Is this network scale free or random?

> There are not so many nodes in this network, but these results look more like a scale free network than like a random
> network given that the number of nodes with the lowest degree is higher than the number of nodes with any other degree.  

Examine the Average clustering coefficient distribution.  Does this network have hierarchical character?

> We would expect to see a much higher clustering coefficient for the nodes with the fewest neighbours if the network was strictly hierarchical.  Remember the y-axis on the Cytoscape graph is not a log-scale.  However, the relationship is not entirely flat either, so it does have some hierarchical structure. 

## 9. Generate a subnetwork of the pancreas-associated proteins

From the original network, we will create a subnetwork of just the proteins that are associated with the pancreas.  One way to do this is to sort on the confidence column in the bottom panel from highest to lowest by clicking on it twice, and then click on the first node with confidence 5, then hold shift and click on the last node with confidence 4 to select them all.  Right click and "Select nodes from selected rows", then File -> New -> Network -> From selected nodes, all edges.  Try Layout -> "Degree sorted circle layout" for a nice visualization of this network.

## 10. Colour the network based on node degree

Now, go back to the original network.  The network analyzer has added columns to the node table that we can use for styling, and the subnetwork has inherited them.  Using the columns that were generated by the network analyzer, colour the network so that you can more easily view the degree of each node.

Since the degree is a numeric value that takes on many values, this time we will use the  'Continuous Mapping' in the style panel.  Double click on the gradient to bring up the 'Continuous Mapping Editor' window.  The colour that will be used for the minimum value is on the left, and the max is on the right.  Double click on the triangles on the top and sides of the gradient to change the colours.  The triangles on the top represent the values at which the data will be clipped -- anything above the right triangle will be set to the max value.  This is useful if you have a small number of values that are significantly higher than the median.  

As you move the triangles and change the colour, the display in the network pane will automatically update -- so this is all easier to do than to explain!  If at any point it doesn't seem to work as expected, it's easiest to just delete the styling and start again. 

What is the node with highest degree?

> Insulin

If you have more time, feel free to play with mapping different network properties onto the network.  

Congratulations, you've reached the end of the exercise! 

## License
Creative Commons Attribution 4.0. 
