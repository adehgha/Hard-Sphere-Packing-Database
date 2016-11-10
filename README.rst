**Table of Contents**:

[TOC]

Hard Sphere Packing Database
=================================
**What is included**: This database has been extracted from the [original work](http://cims.nyu.edu/~holmes/packings.html) of [Professor Miranda Holmes-Cerfon](http://cims.nyu.edu/~holmes/index.html). She has computed all possible hard sphere packings (unless proven otherwise) of clusters with 14 or less particles. In the current work we have only included the clusters with up to 12 particles. Our contribution to this database is the fact that we describe how "iterative" clusters can be broken into "seeds" with smaller size. We have provided unique solutions (splitting to seed clusters) for all the clusters originally provided in Cerfon's database.
We provide a Matlab datafile (.mat) with the following variables:


1- packing: 
-----------

**Contains**: 	3D coordinates of all possible hard sphere packings of clusters with 4 to 12 particles (hence first 3 sub-cells are empty).

**How to access the data**: 
`packing{i}`:  lists all the possible unique hard sphere packings for clusters with size i. `length(packing{i})` provides the number of possible unique hard sphere packings for clusters with size i.

`packing{i}{j}`:   Matrix of size i x 3. Provides the 3D coordinates of the jth unique hard sphere packing of clusters with size i.



2- adj_mat: 
-----------

**Contains**: 	The connectivity matrix (adjacency matrix) of all possible hard sphere packings of clusters of 4 to 12 particles (hence first 3 sub-cells are empty). Size of this cell is identical to that of the `packing` variable (associated with each hard sphere packing there exists a connectivity matrix).

**How to access the data**: 
`adj_mat{i}`:      lists the connectivity matrix for all the possible unique hard sphere packings for clusters with size i.

`adj_mat{i}{j}`:   Square matrix of size i x i. Provides the connectivity matrix for the jth unique hard sphere packing of clusters with size i, (coordinates of which can be found in `packing{i}{j}`). If the element in the mth row and nth column of this matrix is equal to 1 then particle m and n are connected. If the mentioned element is zero then they are not touching.


3- split_solns: 
---------------

**Contains**: 	The type of the hard sphere clusters. Determines if the cluster is a "seed" (can not be divided to smaller hard sphere clusters), or if it is "iterative" (can be split into hard sphere seeds of smaller number of particles). Size of this cell is identical to that of the `packing` variable (associated with each hard sphere packing we provide its type, also if and how it can be split into smaller hard sphere packings).

**How to access the data**: 
`split_solns{i}`:      lists the cluster type (seed or iterative) for all possible unique hard sphere packings of size i.


`split_solns{i}{j}`:   	A cell of size 2. Provides the type of the jth unique hard sphere of clusters with size i, (coordinates of which can be found in `packing{i}{j}`). First field indicates the type of the cluster (seed or iterative). Second field provides a unique solution on how an iterative cluster can be split into smaller seeds. This field will be empty for "seeds" as they can not be split into smaller hard sphere packings. See below for explanation of each of the fields.

`split_solns{i}{j}{1}`: A string with two possible values. "seed" or "iterative".

`split_solns{i}{j}{2}`:	An empty field (for seeds) or a cell structure of size k (for iterative clusters) where k is the number of seed sub-clusters that can split the jth unique hard sphere packing of clusters with size i. If not empty it always contains a cell with multiple sub-clusters. `k = split_solns{i}{j}{2}{1}`.

`split_solns{i}{j}{2}{1}{p}`: Where 0<= p <= k. It includes detailed information about the pth sub-cluster (out of total k sub-clusters) that can be identified in the jth unique hard sphere packing of size i. It always has 5 sub-cells explained below.

`split_solns{i}{j}{2}{1}{p}{1}`: A 1 x q row matrix. where q is the number of particles in the pth sub-cluster. This row matrix provides the indices of the vertices of the sub-cluster to the parent cluster (`packing{i}{j}`). For example if this row matrix looks like `[a, b, c, d]` then this sub-cluster has 4 vertices that are going to be the ath, bth, cth and dth vertex in the parent cluster. The mapping of these vertices are provided in the 5th field of this cell i.e. `split_solns{i}{j}{2}{1}{p}{5}`. See below.


`split_solns{i}{j}{2}{1}{p}{2}`: A q x q square matrix, where q is the number of particles in the pth sub-cluster. This square matrix provides the connectivity matrix of this sub-cluster.

`split_solns{i}{j}{2}{1}{p}{3}`: A string indicating the type of the sub-cluster which is always "seed".

`split_solns{i}{j}{2}{1}{p}{4}`: The id of the found sub-cluster in all the q-sized clusters.


`split_solns{i}{j}{2}{1}{p}{5}`: A 1 x q row matrix, where q is the number of particles in the pth sub-cluster. This row matrix provides a direct mapping between the vertices of the sub-cluster to the parent cluster (`packing{i}{j}`). For example if this row matrix looks like `[b, c, a, d]` then this sub-cluster has 4 vertices in which the 1st vertex maps to the bth vertex in the parent cluster, 2nd vertex maps to c, 3rd vertex maps to a and 4th vertex maps to dth vertex in the parent cluster.


4- un_mat: 
---------------

**Contains**: 	Contains a summary of how clusters split into sub-clusters.  It is a cell of size 12.

**How to access the data**: 
`un_mat{i}`:     A matrix of size r x s, where `r = length(packing{i})`. s is the maximum number of sub-clusters that an iterative cluster of size i can have. Each row of this matrix is associated with an i-sized rigid packing. The values of each row contains the number of vertices that each cluster consists of. For instance if row t of this matrix is equal to:
`un_mat{i}(t, :) = [4, 5 , 5, 0, 0, 0]`
It means that the cluster t, consists of 3 sub-clusters of size 4, 5 and 5 vertices. If a row is all zeros then it means that the cluster associated with that row is a "seed".


# How to cite this work:

If you have used this database in your work, please consider citing the following publications:
1- Holmes-Cerfon, M. C. "Enumerating rigid sphere packings." SIAM Review 58.2 (2016): 229-244. [DOI:10.1137/140982337](http://epubs.siam.org/doi/10.1137/140982337)
2- Banadaki, A. D. & Patala, S. "A Three­Dimensional Polyhedral Unit Model for Grain Boundary Structure in fcc Metals", npj Computational Materials, Under Review (2016).


# Authors:

Arash Dehghan Banadaki <adehgha@ncsu.edu>, Srikanth Patala <spatala@ncsu.edu>

------------------------------------------------------------------------------------------------------

Copyright &copy; 2016,  Arash Dehghan Banadaki and [Srikanth Patala](http://research.mse.ncsu.edu/patala/).
License: GNU-GPL Style.