## Indexing & Search

### ==Indexing==

> [!important] ==Indexing==
> 
> is a data structure technique used to ==locate== and ==quickly access== data in databases to improves database performance by minimizing the number of disc visits required to fulfill a query.

![[Notion/Class Notes/MongoDB/Indexing/attachments/Untitled.png|Untitled.png]]

The `main key` or `candidate key` of the table is duplicated in the ==first column==, which is the Search key. To speed up data retrieval, the values are also kept in ==sorted== order. It should be highlighted that sorting the data is not required.

The ==second column== is the `Data Reference` or `Pointer` which contains a ==set of pointers== holding the ==address of the disk block== where that particular key value can be found.

### Attributes

- **Access Types:** This refers to the type of access such as value-based search, range access…
- **Access Time:** It refers to the time needed to find a particular data element or set of elements
- **Insertion Time:** It refers to the time taken to find the appropriate space and insert new data
- **Deletion Time:** Time taken to find an item and delete it as well as update the index structure
- **Space Overhead:** It refers to the additional space required by the index

> [!info] Indexing in Databases - Set 1 - GeeksforGeeks  
> A Computer Science portal for geeks.  
> [https://www.geeksforgeeks.org/indexing-in-databases-set-1/](https://www.geeksforgeeks.org/indexing-in-databases-set-1/)