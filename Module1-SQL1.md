# SQL 1

## Overview

- 课本章节 5

- [Lecture Slide](https://drive.google.com/file/d/1B5GpXK7nCAv3U8G1CTjwf6-HmMnYSq1w/view)

## Notes

#### SQL Language

- `DML` (`Data Manipulation Language`) 数据操纵语言：

    适用范围：对数据库中的数据进行一些简单操作，如 `insert` , `delete` , `update` , `select` 等.

- `DDL` (`Data Definition Language`) 数据定义语言：

    适用范围：对数据库中的某些对象(例如， `database` , `table` ) 进行管理，如 `Create` , `Alter` 和 `Drop`。

#### RDBMS: Relational Database Management System

`RDBMS` ，关系数据库管理系统。特点是使用一个基于行的表结构，将相关数据元素连接到一起，保证事务完整性，并维护数据的准确性和一致性。同时， `RDBMS` 的另一个显著属性是支持结构化查询语言。


#### SQL DDL

- Create table

    ```
    CREATE TABLE Sailors (
        sid INTEGER,   
        sname CHAR(20), 
        rating INTEGER, 
        age FLOAT
    PRIMARY KEY (sid));
    ```

- Primary Keys

    Primary Key column(s)
    - Provides a unique “lookup key” for the relation
    - Cannot have any duplicate values
    - Can be made up of >1 column

    ```
    CREATE TABLE Boats (
        bid INTEGER,     	
        bname CHAR (20), 
        color CHAR(10), 
    PRIMARY KEY (bid));
    ```

    ```
    CREATE TABLE Reserves (
        sid INTEGER,      
        bid INTEGER, 
        day DATE, 
    PRIMARY KEY (sid, bid, day);
    ```

- Foreign Keys

    ```
    CREATE TABLE Sailors (
        sid INTEGER,   
        sname CHAR(20), 
        rating INTEGER, 
        age FLOAT
    );

    CREATE TABLE Boats (
        bid INTEGER,     	
        bname CHAR (20), 
        color CHAR(10), 
    PRIMARY KEY (bid));

    CREATE TABLE Reserves (
        sid INTEGER,      
        bid INTEGER, 
        day DATE, 
    PRIMARY KEY (sid, bid, day),
    FOREIGN KEY (sid) REFERENCES Sailors,
    FOREIGN KEY (bid) REFERENCES Boats);
    ```

#### SQL DML

- Basic Single-Table Queries

    ```
    SELECT [DISTINCT] <column expression list>FROM <single table>[WHERE <predicate>]
    ```

- SELECT DISTINCT

    ```
    SELECT DISTINCT S.name, S.gpaFROM students SWHERE S.dept = 'CS'
    ```

    - DISTINCT specifies removal of duplicate rows before output

    - Can refer to the students table as “S”, this is called an alias

- ORDER BY

    ```
    SELECT S.name, S.gpa, S.age*2 AS a2FROM Students SWHERE S.dept = 'CS'ORDER BY S.gpa, S.name, a2;
    ```

    - ORDER BY clause specifies output to be sorted
        - Lexicographic ordering
    - Obviously must refer to columns in the output
        - Note the AS clause for naming output columns!

    ```
    SELECT  S.name, S.gpa, S.age*2 AS a2FROM Students SWHERE S.dept = 'CS'ORDER BY S.gpa DESC, S.name ASC, a2;
    ```

    - Ascending order by default, but can be overridden
        - DESC flag for descending, ASC for ascending
        - Can mix and match, lexicographically

- LIMIT

    ```
    SELECT  S.name, S.gpa, S.age*2 AS a2FROM Students SWHERE S.dept = 'CS'ORDER BY S.gpa DESC, S.name ASC, a2LIMIT 3 ;
    ```

    - Only produces the first <integer> output rows
    - Typically used with ORDER BY
        - Otherwise the output is non-deterministic
        - Not a “pure” declarative construct in that case – output set depends on algorithm for query processing

- Aggregates

    ```
    SELECT [DISTINCT] AVG(S.gpa)FROM Students SWHERE S.dept = 'CS';
    ```

    - Before producing output, compute a summary (a.k.a. an aggregate) of some arithmetic expression
    - Produces 1 row of output
        - with one column in this case
    - Other aggregates: SUM, COUNT, MAX, MIN

- GROUP BY

    ```
    SELECT [DISTINCT] AVG(S.gpa), S.deptFROM Students SGROUP BY S.dept
    ```

    - Partition table into groups with same GROUP BY column values
        - Can group by a list of columns
    - Produce an aggregate result per group
        - Cardinality of output = # of distinct group values
    - Note: can put grouping columns in SELECT list

- HAVING

    ```
    SELECT [DISTINCT] AVG(S.gpa), S.deptFROM Students SGROUP BY S.deptHAVING COUNT(*) > 2
    ```

    - The HAVING predicate filters groups
    - HAVING is applied after grouping and aggregation
        - Hence can contain anything that could go in the SELECT list
        - I.e. aggs or GROUP BY columns
    - HAVING can only be used in aggregate queries
    - It’s an optional clause
