Tutorials
=========

We developed an alternative feature extraction method, Marker gene Identification for Cell Type Identity (MICTI), that encodes the cell-type specific expression information to each gene in every single cell. This approach identifies features (genes) that are cell-type specific for a given cell-type in heterogeneous cell population.

Import MICTI module
-------------------

``$from MICTI import *``

Import data 
-----------

We collected single-cell RNA-Seq dataset from six different immune cell types. We performed TPM normaization for each of samples.

``$import pandas as pa``

``$datamatrix=pa.read_csv("dataset.txt", sep="\t", index_col="genes")``


+--------+-------------+-------------+---------------+---------------+--------------+---------------+---------------+----------------+--------------+-------------+
|Genes	 |  GSM2181141 | GSM2181122  |	GSM2181113   |	GSM2180862   | 	GSM2181258  | 	GSM2181201  |	GSM2180840  |	GSM2181133   |	GSM2181089  |	GSM2180853|
+========+=============+=============+===============+===============+==============+===============+===============+================+==============+=============+
|A1BG	 |  0.000000   | 0.043549    |	0.054509     |	0.000000     |	0.000000    |	0.066542    |	0.605715    |	0.651164     |	0.095305    |	0.000000  | 
+--------+-------------+-------------+---------------+---------------+--------------+---------------+---------------+----------------+--------------+-------------+
|A1CF	 |  0.000000   | 0.000000    |	0.000000     |	0.000000     |	0.000000    |	0.000000    |	0.000000    |	0.000000     |	0.000000    |	0.000000  |
+--------+-------------+-------------+---------------+---------------+--------------+---------------+---------------+----------------+--------------+-------------+
|A2M	 |  0.000000   | 0.000000    |	0.000000     |	0.000000     |	0.000000    |	0.000000    |	0.000000    |	0.000000     |	0.000000    |	0.000000  | 
+--------+-------------+-------------+---------------+---------------+--------------+---------------+---------------+----------------+--------------+-------------+
|A2ML1	 |  0.046830   | 0.071208    |	0.018045     |	0.000000     |	0.000000    |	0.023222    |	0.531418    |	0.050903     |	0.098627    |	0.000000  | 
+--------+-------------+-------------+---------------+---------------+--------------+---------------+---------------+----------------+--------------+-------------+
|A4GALT	 |  0.000000   | 0.000000    |	0.000000     |	0.000000     |	0.000000    |	0.000000    |	0.000000    |	0.000000     |	0.000000    |	0.000000  | 
+--------+-------------+-------------+---------------+---------------+--------------+---------------+---------------+----------------+--------------+-------------+
|AAAS	 |  39.244719  | 4.173193    |	28.947780    |	0.000000     |	67.050516   |	97.502654   |	0.000000    |	2.375844     |	88.972850   |	341.262077|
+--------+-------------+-------------+---------------+---------------+--------------+---------------+---------------+----------------+--------------+-------------+
|AACS	 |  0.623697   | 0.401357    |	0.362420     |	0.777686     |	0.270946    |	0.893264    |	0.860927    |	0.546757     |	1.002484    |	0.000000  | 
+--------+-------------+-------------+---------------+---------------+--------------+---------------+---------------+----------------+--------------+-------------+
|AADACL3 |  0.000000   | 0.000000    |	0.000000     |	0.000000     |	0.000000    |	0.000000    |	0.000000    |	0.000000     |	0.000000    |	0.000000  |
+--------+-------------+-------------+---------------+---------------+--------------+---------------+---------------+----------------+--------------+-------------+
|AADAT	 | 0.000000    | 0.000000    |	0.000000     |	0.000000     |	0.000000    |	0.000000    |	0.000000    |	0.000000     |	0.000000    |	0.000000  | 
+--------+-------------+-------------+---------------+---------------+--------------+---------------+---------------+----------------+--------------+-------------+
|AAED1	 | 8.078604    | 8.696563    |	6.825583     |	4.692559     |	0.904554    |	0.456029    |	6.191677    |	12.625448    |	11.592398   | 	10.103919 | 
+--------+-------------+-------------+---------------+---------------+--------------+---------------+---------------+----------------+--------------+-------------+


More information about the samples can be found from the metadata information. Metadata information contains disease stages, tissue catagory, sample source and other important information about the sample/cell. From the metadata table we extracted cell types/sample source in order to classify our cells according to cell type.

``$metadata=pa.read_csv("metadata.txt", sep="\t", index_col="SampleID")``


+-------------+-------------+-------------------------+-----------------------+-----------------------+--------------+----------------------------------------------+----------------+---------------------------------+----------+
| SampleID    |	SubjectID   |	DiseaseCategory	      |	TissueCategory	      |	BamFileName	      |	CellType     |	Description				    |	DiseaseStage |	DiseaseState		       | Ethnicity|	
+=============+=============+=========================+=======================+=======================+==============+==============================================+================+=================================+==========+
|GSM2181141   | No Info	    |	hematologic cancer    |	hematopoietic system  |	EGAX00001437341.bam   |	lymphoblast  |	processed data file = cell_line_FPKM.csv    |	No Info	     |	chronic myeloid leukemia (CML) | No Info  |
+-------------+-------------+-------------------------+-----------------------+-----------------------+--------------+----------------------------------------------+----------------+---------------------------------+----------+
|GSM2181122   |	No Info	    |	hematologic cancer    |	hematopoietic system  | EGAX00001437284.bam   |	lymphoblast  | 	processed data file = cell_line_FPKM.csv    | 	No Info	     |	chronic myeloid leukemia (CML) |No Info   |
+-------------+-------------+-------------------------+-----------------------+-----------------------+--------------+----------------------------------------------+----------------+---------------------------------+----------+
|GSM2181113   |	No Info	    |	hematologic cancer    |	hematopoietic system  |	EGAX00001437257.bam   |	lymphoblast  | 	processed data file = cell_line_FPKM.csv    |	No Info	     | 	chronic myeloid leukemia (CML) |No Info   |
+-------------+-------------+-------------------------+-----------------------+-----------------------+--------------+----------------------------------------------+----------------+---------------------------------+----------+
|GSM2180862   |	No Info	    |	hematologic cancer    |	hematopoietic system  |	EGAX00001437608.bam   |	B cell	     |	processed data file = cell_line_FPKM.csv    |	No Info	     | 	B-cell lymphoma		       |No Info   | 
+-------------+-------------+-------------------------+-----------------------+-----------------------+--------------+----------------------------------------------+----------------+---------------------------------+----------+
|GSM2181258   |	No Info	    |	hematologic cancer    |	hematopoietic system  | EGAX00001439870.bam   |	B cell	     |	processed data file = cell_line_FPKM.csv    |	No Info	     |	B-cell lymphoma		       |No Info   |
+-------------+-------------+-------------------------+-----------------------+-----------------------+--------------+----------------------------------------------+-------------------------------------------------------------+



Now we have cell-type information for each of our samples/cells from the metadata table. So we wanted to get markers for each of the cell-types using MICTI

``$cell_type=list(metadata["CellType"])``

``$set(cell-type)`` ::

	{'B cell',
 	'CD4+ memory T cell',
 	'CD8+ memory T cell',
 	'conventional dendritic cell',
 	'fibroblast',
 	'lymphoblast'}


``$geneName=list(datamatrix.index)``

``$print(geneName[:10])``

``['A1BG', 'A1CF', 'A2M', 'A2ML1', 'A4GALT', 'AAAS', 'AACS', 'AADACL3', 'AADAT', 'AAED1']``

``$cellName=list(datamatrix.columns)``


Creating MICTI object for known cell-types
------------------------------------------

``$mictiObject=MICTI(datamatrix, geneName, cellName, cluster_assignment=cell_type, k=None, th=0, ensembel=False, organisum="hsapiens")``


Lower dimensional data visualization
------------------------------------

``$mictiObject.get_Visualization(method="tsne")``

.. image:: images/MICTI_Plot.pdf

Marker genes for each cluster
~~~~~~~~~~~~~~~~~~~~~~~~~~~~


``$mictiObject.marker_gene_FDR_p_value(0)``


+---------+-----------+--------------+--------------+
| Genes	  | Z_scores  |	Adj P_value	 |  p_value     |
|	      |	          |              |              |
+=========+===========+==============+==============+
|HLA-DRA  | 40.605319 | 0.000000e+00 |  0.000000e+00|
+---------+-----------+--------------+--------------+
|MS4A1	  | 40.199070 | 0.000000e+00 |  0.000000e+00|
+---------+-----------+--------------+--------------+
|TUBB	  | 15.099339 | 0.000000e+00 |  0.000000e+00|
+---------+-----------+--------------+--------------+
|HLA-DPA1 | 14.701781 | 0.000000e+00 |  0.000000e+00|
+---------+-----------+--------------+--------------+
|RPS18	  |61.131416  | 0.000000e+00 |  0.000000e+00|
+---------+-----------+--------------+--------------+

Marker genes for each cluster by P-value and Z-Score threshold
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
 
``$mictiObject.get_markers_by_Pvalues_and_Zscore(1, threshold_pvalue=.01,threshold_z_score=0)``

+-------------+--------------+----------------+----------------+
|Genes	      |	Z_scores     |	fdr	      |	p_value	       |
+-------------+--------------+----------------+----------------+
|CSF2	      | 20.313988    |	0.000000e+00  |	0.000000e+00   |
+-------------+--------------+----------------+----------------+
|IL2RG	      |	12.560409    |	0.000000e+00  |	0.000000e+00   |
+-------------+--------------+----------------+----------------+
|ATP9B	      |	28.123272    |	0.000000e+00  |	0.000000e+00   |
+-------------+--------------+----------------+----------------+
|HIST1H2BK    |	9.118146     |	0.000000e+00  |	0.000000e+00   |
+-------------+--------------+----------------+----------------+
|PATL2	      |	9.055203     |	0.000000e+00  |	0.000000e+00   |
+-------------+--------------+----------------+----------------+
|CTLA4	      |	8.523849     |	0.000000e+00  |	0.000000e+00   |
+-------------+--------------+----------------+----------------+
|CCL20	      |	11.984467    |	0.000000e+00  |	0.000000e+00   |
+-------------+--------------+----------------+----------------+
|MAP3K14      |	32.571130    |	0.000000e+00  |	0.000000e+00   |
+-------------+--------------+----------------+----------------+
|GZMB	      |	17.080777    |	0.000000e+00  |	0.000000e+00   |
+-------------+--------------+----------------+----------------+
|GPR171	      |	10.677701    |	0.000000e+00  |	0.000000e+00   |
+-------------+--------------+----------------+----------------+

Enrichment analysis for identified marker genes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Get gene-over representation enrichmentlysis result for cel-type marker genes in all clusters of cell type

``$enrechment_table=mictiObject.get_sig_gene_over_representation()``

``$enrechment_table[1]`` #CD4+ cells

Creating MICTI object for clustering cells into pre-defined k clusters
----------------------------------------------------------------------

In case, if the cell-type information for each cells is not known, we can perform unsupervided clustering to differentiate cells into predifined k clusters. Here, we use K-means and Gaussian mexture mode for clustering.

Creat MICTI object
~~~~~~~~~~~~~~~~~~

``$mictiObject_1=MICTI(datamatrix, geneName, cellName, cluster_assignment=None, th=0, ensembel=False, organisum="hsapiens")``

Cluster cells into k clusters
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Cluster cells into k=6 clusters using Gaussian mixture model- method="GM", and k-means - method="kmeans"

``$mictiObject_1.cluster_cells(6, method="GM", maxiter=10e3)``

Marker genes per each cluster
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#markers for the third cluster

``$mictiObject_1.get_markers_by_Pvalues_and_Zscore(2, threshold_pvalue=.01, threshold_z_score=0)``

Gene-list Enrichment analysis for cluster marker genes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

``$enrechment_table=mictiObject_1.get_sig_gene_over_representation()``

``$enrechment_table[0]# Enrichment result for the first cluster``




