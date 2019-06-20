User's Guide
============

Creat MICTI Object
------------------

	$MICTI(data,geneNames,cellNames,k=None,cluster_label=None,cluster_assignment=None, th=0,seed=None, ensembel=False, organisum="hsapiens")


Input
~~~~

data
""""
Input data as sparce or dense matrix where the rows are cells and the columns are genes

*geneNames*
"""""""""""
List of gene names

*cellNames*
"""""""""""
List of cell names

*k*
"""
The number of clusters or cell types

*cluster_label*
"""""""""""""""
List of cluster lablees /cell types names

*cluster_assignment*
""""""""""""""""""""
An aaray of cluster assignment for each of cells

*th*
""""
The treshold gene expression value to consider a certain gene is expressed or not

*ensembel*
""""""""""
A boolian value indicating the given gene name is ENSEBEL gene Id or not

*organisum*
"""""""""""
The organisum where dataset belong eg. hsapiens or mmusculus

Output
~~~~~~

The output is the MICTI object

Data visualisation
------------------

``$MICTI.get_Visualization(dim=2,method="tsne")``

Input
~~~~~

*dim*
"""""
The number of dimension for visualisation dim=2 or dim=3

*method*
""""""""
The method used for low dimensional visualisation, method="PCA" or method="tsne"

Output
~~~~~~
Returns none. Desplays the lower dimensional representation of the dataset

Clustering cells
----------------

``$MICTI.cluster_cells(numberOfCluster, method="kmeans", maxiter=500)``

Input
~~~~~

*numberOfCluster*
"""""""""""""""""
The number of clusters

*method*
""""""""
The method used for clustering. There are two options, ie. method="kmeans" for kmeans clustering or method="GM" gaussian mixture model for clustering

*maxiter*
"""""""""
The maximum iteration that the k-means or Gaussian mixture algorithm takes in the clustering process.

Output
~~~~~~

Returns None, assigning each cells into k clusters 

Cell-type marker genes
----------------------

``$MICTI.marker_gene_FDR_p_value(clusterNo)``

Input
~~~~~

*clusterNo*
"""""""""""
The cluster number. Each clusters are identified by number. For example, if there are six clusters/cell-types, the cluster numbers are from 0-5.

Output
~~~~~~

Returns a table with Z-score, p-value and FDR p-value for each of the genes.

significant cluster markers
---------------------------

``$MICTI.get_markers_by_Pvalues_and_Zscore(clusterNo,threshold_pvalue=.01, threshold_z_score=0)``

Input
~~~~~

*clusterNo*
"""""""""""
The cluster number. Each clusters are identified by number. For example, if there are six clusters/cell-types, the cluster numbers are from 0-5.

*threshold_pvalue*
""""""""""""""""""
The threshold FDR p-value. Genes/Markers with less than the threshold FDR p-value are selected.

*threshold_z_score*
"""""""""""""""""""
The threshold Z-scores. Genes/markers with greater than the threshold z-score are selected.

Output
~~~~~~

Returns a table with Z-score, p-value and FDR p-value of significantlly cell-type/cluster marker genes filtered by FDR Pvalue and Z-score.

Gene-list enrichment analysis
-----------------------------

``$MICTI.get_sig_gene_over_representation()``

Input
~~~~~
None

Output
~~~~~~
Returns a list with gene-list enrichment analysis result for each of cell-type/cluster marker genes


