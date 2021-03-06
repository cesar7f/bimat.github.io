---
layout: page
title:  Configuration
date:   25-02-17 21:12:57
category: inst
order: 1
---
 
### Default Values: Options.m File

Most of the <tt>BiMat</tt> functions can work without the need of parameters by the user. However, if the user does
not specify the required arguments, BiMat will use the default values. These values
are specified on the file <tt>main/Options.m</tt> that the user can modify according to his needs. The next sections indicate
the default parameters of <tt>BiMat</tt>

#### Statistics

* **Statistical Significance:** A two-tail test is the default way of testing for
significance in <tt>BiMat</tt>. Notice that the user can perform a one-tail test by just duplicating 
the values below:
  * <tt>P_VALUE = 0.05</tt>: The $p$-value for testing statistical significance using a percentile test approach.
	Anything outside the percentile range $[100(p/2), 100(1-p/2)]$ will be considered statistically significant.<br><br>
  * <tt>Z_SCORE = 1.96</tt>: The $z$-score for testing statistical significance using a $z$-test approach.
	Anything outside the $z$-score range $[-|z|,|z|]$ will be considered statistically significant. Notice that the default value
	corresponds to a 5% two tailed test.<br><br>
* **Null Models:**
  * <tt>DEFAULT_NULL_MODEL = @NullModels.EQUIPROBABLE</tt>: The default function for creating random
	networks (see [Null Models](/BiMat/stats/null_models.html "Null Models") for detailed description of the avalaible null models in <tt>BiMat</tt>).<br><br> 
  * <tt>ALLOW_ISOLATED_NODES = true</tt>: When the network is sparse, a random network may be created
	with nodes with no links at all (matrix with empty rows or columns). <tt>BiMat</tt> by default  
	allows these kinds of random networks for performing the statistical test. However, the user may want to 
	change this value to <tt>false</tt>to avoid the creation of this kind of random networks. However, the user must be aware
	that the time required for creating a random network without empty nodes will grow with the sparsity of the matrix.<br><br>
  * <tt>TRIALS_FOR_NON_EMPTY_NODES = 1000</tt>: This value is only used when the user changes
	the value of the previous parameter to <tt>false</tt>. In some extreme cases (a very sparse network),
	<tt>BiMat</tt> will not be able to find a random network without empty nodes. Hence, in order to avoid infinite
	loops, <tt>BiMat</tt> will stop looking for them after the number of trials specified in this parameter. 
	If <tt>BiMat</tt> can not create a random network without empty nodes before this number of trials, <tt>BiMat</tt>
	will just create a random network without this constraint and will print the next message in 
	the <tt>Matlab</tt> command line:
	<pre class="codeoutput">
	Warning: Not possible to create a matrix with non isolated nodes.
	The random matrix was created without this constraint instead.
	Consider to modify Options.ALLOW_ISOLATED_NODES and/or Options.INCLUDE_EMPTY_NODES
	</pre>
  * <tt>INCLUDE_EMPTY_NODES = true</tt>: Sometimes the user may have data with empty nodes (a matrix
	with empty rows and/or columns). Depending on the value of this parameter <tt>BiMat</tt> will choose 
	between keeping these nodes (<tt>true</tt>)  or deleting them from the adjacency matrix (<tt>false</tt>).
	Further, the user must be aware that this choice affects the statistical tests.<br><br>
  * <tt>REPLICATES = 100</tt>: The amount of replicates that <tt>BiMat</tt> performs in order to test
	for statistical significance. The value of <tt>100</tt> was chosen with the idea of getting quick
	results. However, the user must be aware that this value is not appropriate for accurate
	testing. The right value will depend on the size and sparsity of the network to be tested.<br><br>

####Algorithms
All the next parameters refer to algorithms behavior. The user
can change the values here, or he can change the parameters dynamically by modifying the corresponding
properties in the <tt>BipartiteModularity</tt> or <tt>Nestedness</tt> instance.

* **Nestedness:**
  * <tt>NESTEDNESS_ALGORITHM = @NestednessNODF</tt>: <tt>BiMat</tt> has two metrics for evaluating
	nestedness. Possible values are (see [Nestedness](/BiMat/alg/nestedness.html "Nestedness")
	for detailed description of the avalaible metrics in <tt>BiMat</tt>):
        - <tt>@NestednessNODF</tt>
        - <tt>@NestednessNTC</tt> <br><br>

* **Modularity:**
  * <tt>MODULARITY_ALGORITHM = @AdaptiveBrim</tt>: <tt>BiMat</tt> has three algorithms
	for optimizing the modularity equation and hence find the module configuration of the network.
	 Possible values are 
	(see [Modularity](/BiMat/alg/modularity.html "Modularity") for detailed description of the avalaible algorithms in <tt>BiMat</tt>):
        -  <tt>@AdaptiveBrim</tt>
        -  <tt>@LPBrim</tt>
        -  <tt>@LeadingEigenvector</tt> <br><br> 
  * <tt>OPTIMIZE_COMPONENTS = false</tt>: Modularity is a function that depends in the global information
	of the network. However, sometimes, the user may have a network which is not connected (it has
	isolated components). By using the default value <tt>false</tt>, <tt>BiMat</tt> will optimize the modularity
	value at the entire adjacency matrix, while by using the value <tt>true</tt>, <tt>BiMat</tt> will optimize
	the modularity at the component level. Optimizing at the component level may decrease the 
	global modularity value, though the number of communities may increase and be finer.<br><br>
  * <tt>TRIALS_MODULARITY = 20</tt>: The results of the modularity algorithms depend strongly
	on some initial random assignment of the communities. Therefore, <tt>BiMat</tt> restarts the algorithm using this number of times.
        


