---
layout: post
title:  "Добавление хостов и папок в cacti средствами python"
date:   2011-10-10 20:20:50 +0400
categories: cacti python
tags: cacti python
---

# Добавление хостов и папок в cacti средствами python
```
GRANT ALL ON cacti3.* TO cacti@localhost IDENTIFIED BY '4QDrBrp4uCUuuEQ5';
flush privileges;
```

```
GRANT ALL ON cacti3.* TO cacti@localhost IDENTIFIED BY '4QDrBrp4uCUuuEQ5';
```

```
id   graph_tree_id local_graph_id rra_id    title                                     host_id                       order_key                                                                                                                                                                  host_grouping_type  sort_children_type
| 3703 |             1 |           3654 |      1 |                                                 |       0 | 037007020017000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  0 |                  0 |
| 3704 |             1 |           3655 |      1 |                                                 |       0 | 037007020018000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  0 |                  0 |





| 3573 |             1 |           3540 |      1 |                                                 |       0 | 037007003000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  0 |                  0 |
| 3574 |             1 |              0 |      0 | Ring01                                          |       0 | 037007004000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  1 |                  1 |
| 3575 |             1 |              0 |      0 | Ring02                                          |       0 | 037007005000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  1 |                  1 |
| 3576 |             1 |              0 |      0 | Ring03                                          |       0 | 037007006000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  1 |                  1 |
| 3577 |             1 |              0 |      0 | Ring04                                          |       0 | 037007007000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  1 |                  1 |
| 3578 |             1 |              0 |      0 | Ring05                                          |       0 | 037007008000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  1 |                  1 |
| 3579 |             1 |              0 |      0 | Ring06                                          |       0 | 037007009000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  1 |                  1 |
| 3580 |             1 |              0 |      0 | Ring07                                          |       0 | 037007010000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  1 |                  1 |
| 3581 |             1 |              0 |      0 | Ring08                                          |       0 | 037007011000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  1 |                  1 |
| 3582 |             1 |              0 |      0 | Ring09                                          |       0 | 037007012000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  1 |                  1 |
| 3583 |             1 |              0 |      0 | Ring10                                          |       0 | 037007013000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  1 |                  1 |
| 3584 |             1 |              0 |      0 | Ring11                                          |       0 | 037007014000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  1 |                  1 |
| 3585 |             1 |              0 |      0 | Ring12                                          |       0 | 037007015000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  1 |                  1 |
| 3586 |             1 |              0 |      0 | Ring13                                          |       0 | 037007016000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  1 |                  1 |
| 3587 |             1 |              0 |      0 | Ring14                                          |       0 | 037007017000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  1 |                  1 |
| 3588 |             1 |              0 |      0 | Ring15                                          |       0 | 037007018000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  1 |                  1 |
| 3589 |             1 |              0 |      0 | Ring16                                          |       0 | 037007019000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  1 |                  1 |
| 3590 |             1 |              0 |      0 | Other                                           |       0 | 037007020000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  1 |          
| 3591 |             1 |           3541 |      1 |                                                 |       0 | 037007004001000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  0 |                  0 |

```


```
LOCK TABLES `graph_tree` WRITE;
/*!40000 ALTER TABLE `graph_tree` DISABLE KEYS */;
INSERT INTO `graph_tree` VALUES (1,1,'Default Tree'),(5,1,'quicktree'),(6,1,'multicast-tree'),(7,1,'ping'),(8,1,'Regard'),(9,1,'Phys-Nodes');
/*!40000 ALTER TABLE `graph_tree` ENABLE KEYS */;
UNLOCK TABLES;
```


```
DROP TABLE IF EXISTS `graph_tree_items`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!40101 SET character_set_client = utf8 */;
CREATE TABLE `graph_tree_items` (
  `id` mediumint(5) unsigned NOT NULL AUTO_INCREMENT,
  `graph_tree_id` smallint(5) unsigned NOT NULL DEFAULT '0',
  `local_graph_id` mediumint(8) unsigned NOT NULL DEFAULT '0',
  `rra_id` smallint(8) unsigned NOT NULL DEFAULT '0',
  `title` varchar(255) DEFAULT NULL,
  `host_id` mediumint(8) unsigned NOT NULL DEFAULT '0',
  `order_key` varchar(100) NOT NULL DEFAULT '0',
  `host_grouping_type` tinyint(3) unsigned NOT NULL DEFAULT '1',
  `sort_children_type` tinyint(3) unsigned NOT NULL DEFAULT '1',
  PRIMARY KEY (`id`),
  KEY `graph_tree_id` (`graph_tree_id`),
  KEY `host_id` (`host_id`),
  KEY `local_graph_id` (`local_graph_id`),
  KEY `order_key` (`order_key`)
) ENGINE=MyISAM AUTO_INCREMENT=3705 DEFAULT CHARSET=utf8;
/*!40101 SET character_set_client = @saved_cs_client */;
```



```
| 3730 |             1 |              0 |      0 | subdistrict1                                    |       0 | 037003010000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  1 |                  1 |
| 3731 |             1 |              0 |      0 | subdistrict2                                    |       0 | 037003011000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  1 |                  1 |
| 3732 |             1 |              0 |      0 | subdistrict3                                    |       0 | 037003012000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  1 |                  1 |
| 3733 |             1 |              0 |      0 | Ring01                                          |       0 | 037003010001000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  1 |                  1 |
| 3734 |             1 |              0 |      0 | Ring02                                          |       0 | 037003010002000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  1 |                  1 |
| 3735 |             1 |              0 |      0 | Ring03                                          |       0 | 037003010003000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  1 |                  1 |
| 3736 |             1 |              0 |      0 | Ring04                                          |       0 | 037003010004000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  1 |                  1 |
| 3737 |             1 |           3691 |      1 |                                                 |       0 | 003063000000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  0 |                  0 |
| 3738 |             1 |           3692 |      1 |                                                 |       0 | 003064000000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  0 |                  0 |
| 3739 |             1 |           3693 |      1 |                                                 |       0 | 003065000000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  0 |                  0 |
| 3740 |             1 |           3688 |      1 |                                                 |       0 | 003066000000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  0 |                  0 |
| 3741 |             1 |           3689 |      1 |                                                 |       0 | 003067000000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  0 |                  0 |
| 3742 |             1 |           3690 |      1 |                                                 |       0 | 003068000000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  0 |                  0 |
| 3743 |             1 |           3696 |      1 |                                                 |       0 | 003069000000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  0 |                  0 |
| 3744 |             1 |           3697 |      1 |                                                 |       0 | 003070000000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  0 |                  0 |
| 3745 |             1 |           3694 |      1 |                                                 |       0 | 003071000000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  0 |                  0 |
| 3746 |             1 |           3695 |      1 |                                                 |       0 | 003072000000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  0 |                  0 |
| 3747 |             1 |           3699 |      1 |                                                 |       0 | 005004010011011000000000000000000000000000000000000000000000000000000000000000000000000000 |                  0 |                  0 |
| 3748 |             1 |           3700 |      1 |                                                 |       0 | 005004010011012000000000000000000000000000000000000000000000000000000000000000000000000000 |                  0 |                  0 |
| 3749 |             1 |           3701 |      1 |                                                 |       0 | 005004010011013000000000000000000000000000000000000000000000000000000000000000000000000000 |                  0 |                  0 |
| 3750 |             1 |           3698 |      1 |                                                 |       0 | 005004010011014000000000000000000000000000000000000000000000000000000000000000000000000000 |                  0 |                  0 |
| 3751 |             1 |              0 |      0 | Ring05                                          |       0 | 037003010005000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  1 |                  1 |

```

```
MariaDB [cacti3]> select * from graph_tree_items where title="16d";
+------+---------------+----------------+--------+-------+---------+--------------------------------------------------------------------------------------------+--------------------+--------------------+
| id   | graph_tree_id | local_graph_id | rra_id | title | host_id | order_key                                                                                  | host_grouping_type | sort_children_type |
+------+---------------+----------------+--------+-------+---------+--------------------------------------------------------------------------------------------+--------------------+--------------------+
| 1078 |             1 |              0 |      0 | 16d   |       0 | 037003000000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  1 |                  1 |
+------+---------------+----------------+--------+-------+---------+--------------------------------------------------------------------------------------------+--------------------+--------------------+
1 row in set (0.00 sec)
```

Just don't provide the name of the column, it will default to a the next auto_increment value.

cursor.execute("INSERT INTO association (nom, service, theme) VALUES (%s, %s, %s)", (nom, service, theme))

As a side note, I generally recommend against 2-letter generic column names like "id". Later you'll go insane trying to grep for all the places where "id" is used. :-)



```
 subdistrict1                                    |       0 | 03700301
Ring01                                          |       0 | 037003010001


subdistrict2                                    |       0 | 037003011000
 Ring01                                          |       0 | 037003011001
 ```
 
 
 
 
 
 
 
 ```
 select * from graph_tree_items where title="subdistrict1";
```
 
 
 
 ```
 db = MySQLdb.connect(host="localhost", user="cacti", passwd="4QDrBrp4uCUuuEQ5", db="cacti3")
cursor = db.cursor()
result = cursor.fetchall()
 ```
 37003010004
 ```
 for i in 
 
 
 for row in result:
        print(row[6][1:12])
        
         (f for row in result if os.stat(f).st_size > 6000)
        
        
 
 (f for f in result if os.stat(f).st_size > 6000)
 
 [f for f in glob.glob('*.py') if os.stat(f).st_size > 6000]
 ```
 
 
 
 
 
 
 ```
 spisok = [0,10,20,30,40,50,60,70,80,90]
 i = 0
 for element in spisok:
	spisok[i] = element + 2
	i = i + 1
 
 spisok
[2, 12, 22, 32, 42, 52, 62, 72, 82, 92]
```

```
print(result[0][6][1:12])
print(result[0][6][1:10])

#370030100
037003010005000000000000000000000000000000000000000000000000000000000000000000000000000000

element=result[0][6][1:12]

for (i=1; i<=28, i++)
    element[i] = element + 1

stroka='Rings{number:02}'.format(number=3)


In [29]: a
Out[29]: (4, 5, 6, 7, 8, 9, 10)

b = []
for element in a:
   'Ring{number:02}'.format(number=element))
  
Ring04
Ring05
Ring06
Ring07
Ring08
Ring09
Ring10




a = (4, 5, 6, 7, 8, 9, 10)
a = xrange (4, 10)
for a in xrange (4:28)
```



```
for element in range(len(index_list)):
    a_list.append((1,0,0,'Ring{number:02}'.format(number=element),0,'037003010000000000000000000000000000000000000000000000000000000000000000000000000000000000',1,1))
for element in range(len(index_list)):
    a_list.append((1,0,0,'Ring{number:02}'.format(number=element),0,'037003010000000000000000000000000000000000000000000000000000000000000000000000000000000000',1,1))
```
   

```
stroka= "0"+result[0][6][1:10]+'{number:02}'.format(number=1)+"0000000000000000000000000000000000000000000000000000000000000000000000000000000"

In [126]: stroka
Out[126]: '0370030100010000000000000000000000000000000000000000000000000000000000000000000000000000000'
  
    
    
for element in range(6,27):
     a_list.append((1,0,0,'Ring{number:02}'.format(number=element),0,"0"+result[0][6][1:10]+'{number:02}'.format(number=element)+"0000000000000000000000000000000000000000000000000000000000000000000000000000000",1,1))
   ....:    

   
   

 for element in range(6,27):
    a_list.append((1,0,0,'Ring{number:02}'.format(number=element),0,"0"+result[0][6][1:10]+'{number:02}'.format(number=element)+"0000000000000000000000000000000000000000000000000000000000000000000000000000000",1,1))
   
   
   
    
    
result[0][6][1:12]
index_list = list(range (6,26))
a_list = []
for element in range(6,26)):
   a_list.append((graph_tree_id, local_graph_id, rra_id, 'Ring{number:02}'.format(number=element), host_id, ORDER_KEY, host_grouping_type, sort_children_type))

   
   
   
   
   

 for element in index_list:
       b.append(('Ring{number:02}'.format(number=element)))
   ....:     

Out[45]: ['Ring04', 'Ring05', 'Ring06', 'Ring07', 'Ring08', 'Ring09', 'Ring10']
```  
    
    

    
  ```  
 a_tuple = (graph_tree_id, local_graph_id, rra_id, TITLE, host_id, ORDER_KEY, host_grouping_type, sort_children_type)
 a_tuple
 a_list=list(a_tuple)
```
```
 Сработало
 cursor.executemany( """INSERT INTO graph_tree_items (graph_tree_id, local_graph_id, rra_id, title, host_id, order_key, host_grouping_type, sort_children_type) VALUES (%s, %s, %s, %s, %s, %s, %s, %s)""", a_list)
 
 
 
 
 cursor.execute("INSERT INTO graph_tree_items (graph_tree_id, local_graph_id, rra_id, title, host_id, order_key, host_grouping_type, sort_children_type) VALUES (%d, %d, %d, %s, %d, %s, %d, %d)", (graph_tree_id, local_graph_id, rra_id, title, host_id, order_key, host_grouping_type, sort_children_type))

  cursor.execute("INSERT INTO graph_tree_items (graph_tree_id, local_graph_id, rra_id, title, host_id, order_key, host_grouping_type, sort_children_type) VALUES (%d, %d, %d, %s, %d, %s, %d, %d)", a_list)
 
 cursor.executemany( """INSERT INTO graph_tree_items (graph_tree_id, local_graph_id, rra_id, title, host_id, order_key, host_grouping_type, sort_children_type) VALUES (%d, %d, %d, %s, %d, %s, %d, %d)""", a_list)
    
    
     c.executemany(
      """INSERT INTO breakfast (name, spam, eggs, sausage, price)
      VALUES (%s, %s, %s, %s, %s)""", 
      [
      ("Spam and Sausage Lover's Plate", 5, 1, 8, 7.95 ),
      ("Not So Much Spam Plate", 3, 2, 0, 3.95 ),
      ("Don't Wany ANY SPAM! Plate", 0, 4, 3, 5.95 )
      ] )
 
 
 
 
 a_list
Out[99]: 
[(1,
  0,
  0,
  'subdistrict4',
  0,
  '037003013000000000000000000000000000000000000000000000000000000000000000000000000000000000',
  1,
  1)]

  cursor.executemany( """INSERT INTO graph_tree_items (graph_tree_id, local_graph_id, rra_id, title, host_id, order_key, host_grouping_type, sort_children_type) VALUES (%s, %s, %s, %s, %s, %s, %s, %s)""", a_list)
  
 
 
 >>> res = []

>>> for x in xrange(1, 25, 2):

... res.append(x)

...

>>> print res
```

В общем-то, полученный результат - целиком нас устраивает всем, кроме длинной записи. тут-то на помощь и придет наш "сахарок". В самом простом виде, он обычно
```
>>> res = [x for x in xrange(1, 25, 2)]

>>> print res
 
 
  3730 |             1 |              0 |      0 | subdistrict1                                    |       0 | 037003010000000000000000000000000000000000000000000000000000000000000000000000000000000000 |                  1 |                  1 |
  ```