#AWS
Redshift is a solution for big data from Amazon.  Once you’ve created a data warehouse, called a cluster, you can use SQL tools to perform analysis fast.  Really fast.


## Relational Database and SQL
The data is stored in a relational database and is queried using SQL as a query language.  Queries are optimised and enhanced before being distributed among the nodes.


## Clusters and nodes
When a query is executed it is distributed among nodes. The nodes get the results in parallel and present a single consolidated result to the leader node.  Clusters can be scaled up and down as required meaning costs can be kept under control depending on demand.


## Compressed Column Storage Technology
The data is stored column-wise as opposed to row-wise supporting high compression and in-memory operations. Columnar data stores are effectively an index for every column.  Data of the same type with similar values are organised next to each other.  Unlike other database solutions, the query doesn’t have to scan through every row and produces results much faster.
