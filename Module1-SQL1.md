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


#### SQL DML