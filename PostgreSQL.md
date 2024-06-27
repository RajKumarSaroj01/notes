## PostgreSQL
* It's ORDMS, object-oriented relational database management system
* Default connection is 115, 15 for superuser and 100 for normal user. It can be modified as per requirement. 
* Out of the box data types 
    * interval
    * point , to store geo-graphical location
* Window function
    * It can be used by ```OVER``` clause with ```PARTITION BY ```clause    
    * It is used to get the  task done on subset of rows unlike ```GROUP BY``` which is used to get the task done on whole table row.
    * Example: Avg order price across cities in given year
    ``` SELECT orderid, price, order_date,city, avg(price) OVER (PARTITION BY city) FROM order_table where year(order_date)='2020'; ```
    * Above query will list each row with avg order price based on city 

   
    | randomeId | 170 | 01-01-2020 | ABC | 256.666 |

    | randomeId | 200 | 02-11-2020 | ABC | 256.666 |

    | randomeId | 400 | 12-06-2020 | ABC | 256.666 |
    
    | randomeId | 100 | 10-01-2020 | XYZ | 100.000 |

    | randomeId | 150 | 07-05-2020 | XYZ | 100.000 |
    
    | randomeId | 50 | 01-03-2020 | XYZ | 100.000 |
    
    | randomeId | 10 | 25-02-2020 | MNQ | 20.000 |

    | randomeId | 30 | 21-08-2020 | MNQ | 20.000 | 

#### when to use PostgreSQL
#### CAP theorem 
#### ACID property 
#### how it's highly secure 
#### multiversion concurrency support (MVCC)
#### which data structure uses for indexing
#### internal architecture
#### how it stores each data type
#### how it store row and col
#### query execution order means order of when, order by , limit etc.. is it similar to mysql 

#### master slave architecture, how and when replication happens , replication lag  

#### impact of more number of index in table
#### why the default  connection is less, so on default connection less number of servers can be connected problem while scalling the server 