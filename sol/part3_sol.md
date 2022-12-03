# HW4 Part 3 Solutions

**Q1**:
This query plan first runs an index scan on the BTree index `iowa_zip_btree`, with condition `zipcode = 10027`.
The results are then fed into the heap scan, which subsequently sorts the tuples by the data pages they reside in, 
and reads the tuples from those data pages. 

Both B+ tree and hash index can handle equality conditions. Postgres prefer tree index rather than hash on equality comparisons could be many reasons. Bucket chains could be one. Typically databases will use trees since they are heavily optimized as compared to random accesses for hash indexes.
  
 **Q2**:
This is because the estimated number is only an educated guess based on the table's metadata. 

The estimate is usually `NCARD * selectivity`, where `NCARD` is the number of rows in the table and `selectivity` varies for different values and ranges. As an example, one possible value for selectivity is `1/ICARD`, where `ICARD` is the number of distinct values of the `zipcde` row. This can differ a lot from actual number of rows in the result.

Estimated costs and row counts might vary slightly because they are random samples rather than exact, and because costs are inherently somewhat platform-dependent.

**Q3**:
The query plan uses the hash index. This is an equality constraint, and we only require one row as output. 
Typically databases will use trees since they are heavily optimized as compared to random accesses for hash indexes.
However, when the query result has very low `LIMIT` number (e.g. `LIMIT 1`) will hash index win over btree. Since there are so few that the extra gaim of sorting the row locations is not worth it.

**Q4**:
The difference lies in the selectivity of these two queries. Q4A has higher selectivity, Btree index access path will help in
eliminating unnecessary disk IOs.   
However, Q4B covers basically the whole zipcode range, which suggests the output would be nearly all the tuples in the tables, so it is better to do sequential scan for reducing disk IO, since Btree requires 1 IO for accessing 1 records, other than 1 page with Sequential Scan.  
Same thing could be told from with cost statistics yield by `EXPLAIN` query.

**Q5**:
Q5A accesses `iowa_store_tree` index. Q5B use `iowa_store_item_vendor_dt_tree`. They are not the same, but still tree index.
We can see Q5A has around 0.5 selectivity, and Q5B has better selectivity, thus disk IO can be saved greatly compared with sequential scan. Btree allows Bitmap Index Scan, which will save a lot unnecessary random IOs.

Bitmap Scans are very different from plain Index Scans. An Index Scan simply scans through an index and fetches tuples that satisfy a condition one by one. Thus each tuple would incur a separate access to a data page. On the other hand, a Bitmap Scan collects all pointers to tuples matching a condition, sorts them by the data pages they are stored in, and then fetches those tuples in one go. This improves the locality of page accesses. 

**Q6**:
It will take more time for records update/insertion, since indexes force some ordered data structure, which is costly when update/insertion.
