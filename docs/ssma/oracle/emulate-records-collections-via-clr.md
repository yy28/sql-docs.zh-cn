---
title: 通过 CLR UDT 模拟记录和集合
description: 介绍了如何使用 SQL Server 公共语言运行时（CLR）用户定义数据类型（UDT）来模拟 Oracle 记录和集合，SQL Server 迁移助手（SSMA）用于 Oracle。
authors: nahk-ivanov
ms.service: ssma
ms.devlang: sql
ms.topic: article
ms.date: 1/22/2020
ms.author: alexiva
ms.openlocfilehash: 39a7e8d59425db7ce2d7e81083012321caac35ef
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "76762811"
---
# <a name="emulating-records-and-collections-via-clr-udt"></a>通过 CLR UDT 模拟记录和集合

本文介绍了如何使用 SQL Server 的公共语言运行时（CLR）用户定义数据类型（UDT）来模拟 Oracle 记录和集合，SQL Server 迁移助手（SSMA）。

## <a name="declaring-record-or-collection-types-and-variables"></a>声明记录或集合类型和变量

SSMA 创建三个基于 CLR 的 Udt：

* `CollectionIndexInt`
* `CollectionIndexString`
* `Record`

此`CollectionIndexInt`类型用于模拟按整数索引的集合，如`VARRAY`s、嵌套表和基于整数键的关联数组。 `CollectionIndexString`类型用于按字符键编制索引的关联数组。 Oracle 记录功能由`Record`类型进行模拟。

记录或集合类型的所有声明都转换为此 Transact-sql 声明：

```sql
declare @Collection$TYPE varchar(max) = '<type definition>'
```

下面`<type definition>`是唯一标识源 PL/SQL 类型的描述性文本。

请考虑以下示例：

```sql
DECLARE
    TYPE Manager IS RECORD
    (
        mgrid integer,
        mgrname varchar2(40),
        hiredate date
    );

    TYPE Manager_table is TABLE OF Manager INDEX BY PLS_INTEGER;

    Mgr_rec Manager;
    Mgr_table_rec Manager_table;
BEGIN
    mgr_rec.mgrid := 1;
    mgr_rec.mgrname := 'Mike';
    mgr_rec.hiredate := sysdate;

    select
        empno,
        ename,
        hiredate
    BULK COLLECT INTO
        mgr_table_rec
    FROM
        emp;
END;
```

使用 SSMA 进行转换时，它将成为以下 Transact-sql 代码：

```sql
BEGIN
    DECLARE
        @CollectionIndexInt$TYPE varchar(max) =
            ' TABLE INDEX BY INT OF ( RECORD ( MGRID INT , MGRNAME STRING , HIREDATE DATETIME ) )'

    DECLARE
        @Mgr_rec$mgrid int,
        @Mgr_rec$mgrname varchar(40),
        @Mgr_rec$hiredate datetime2(0),
        @Mgr_table_rec dbo.CollectionIndexInt =
            dbo.CollectionIndexInt::[Null].SetType(@CollectionIndexInt$TYPE)

    SET @mgr_rec$mgrid = 1
    SET @mgr_rec$mgrname = 'Mike'
    SET @mgr_rec$hiredate = sysdatetime()

    SET @mgr_table_rec = @mgr_table_rec.RemoveAll()
    SET @mgr_table_rec =
        @mgr_table_rec.AssignData(
            ssma_oracle.fn_bulk_collect2CollectionComplex((
                SELECT
                    CAST(EMP.EMPNO AS int) AS mgrid,
                    EMP.ENAME AS mgrname,
                    EMP.HIREDATE AS hiredate
                FROM dbo.EMP
                FOR XML PATH
            ))
        )
END
```

此处，由于`Manager`表与数值索引（`INDEX BY PLS_INTEGER`）相关联，因此所使用的相应 t-sql 声明为类型。 `@CollectionIndexInt$TYPE` 如果表与字符集索引相关联（例如`VARCHAR2`），则相应的 t-sql 声明的类型`@CollectionIndexString$TYPE`为：

```sql
-- Oracle
TYPE Manager_table is TABLE OF Manager INDEX BY VARCHAR2(40);

-- SQL Server
@CollectionIndexString$TYPE varchar(max) =
    ' TABLE INDEX BY STRING OF ( RECORD ( MGRID INT , MGRNAME STRING , HIREDATE DATETIME ) )'
```

Oracle 记录功能只能通过`Record`类型进行模拟。

每`CollectionIndexInt`个类型、 `CollectionIndexString`、和`Record`都有一个返回空实例的`[Null]`静态属性。 调用`SetType`方法接收特定类型的空对象（如上面的示例所示）。

## <a name="constructor-call-conversions"></a>构造函数调用转换

构造函数表示法只能用于嵌套表和`VARRAY`，因此所有显式构造函数调用都使用`CollectionIndexInt`类型进行转换。 空构造函数调用通过`SetType`调用的`CollectionIndexInt`null 实例调用。 `[Null]`属性返回空实例。 如果构造函数包含元素的列表，则按顺序应用特殊方法调用以将值添加到集合中。

例如：

```sql
-- Oracle

DECLARE
    TYPE nested_type IS TABLE OF VARCHAR2(20);
    TYPE varray_type IS VARRAY(5) OF INTEGER;

    v1 nested_type;
    v2 varray_type;
BEGIN
   v1 := nested_type('Arbitrary','number','of','strings');
   v2 := varray_type(10, 20, 40, 80, 160);
END;

-- SQL Server

BEGIN
    DECLARE
        @CollectionIndexInt$TYPE varchar(max) = ' VARRAY OF INT',
        @CollectionIndexInt$TYPE$2 varchar(max) = ' TABLE OF STRING',
        @v1 dbo.CollectionIndexInt,
        @v2 dbo.CollectionIndexInt

    SET @v1 =
        dbo.CollectionIndexInt::[Null]
            .SetType(@CollectionIndexInt$TYPE$2)
            .AddString('Arbitrary')
            .AddString('number')
            .AddString('of')
            .AddString('strings')

   SET @v2 =
       dbo.CollectionIndexInt::[Null]
            .SetType(@CollectionIndexInt$TYPE)
            .AddInt(10)
            .AddInt(20)
            .AddInt(40)
            .AddInt(80)
            .AddInt(160)
END
```

## <a name="referencing-and-assigning-record-and-collection-elements"></a>引用和分配记录和集合元素

每个 Udt 都具有一组使用各种数据类型的元素的方法。 例如， `SetDouble`方法会将一个`float(53)`值分配给记录或集合，并且`GetDouble`可以读取此值。 下面是方法的完整列表：

```sql
GetCollectionIndexInt(@key <KeyType>) returns CollectionIndexInt;
SetCollectionIndexInt(@key <KeyType>, @value CollectionIndexInt) returns <UDT_type>;
GetCollectionIndexString(@key <KeyType>) returns CollectionIndexString;
SetCollectionIndexString(@key <KeyType>, @value CollectionIndexString) returns <UDT_type>;
Record GetRecord(@key <KeyType>) returns Record;
SetRecord(@key <KeyType>, @value Record) returns <UDT_type>;
GetString(@key <KeyType>) returns nvarchar(max);
SetString(@key <KeyType>, @value nvarchar(max)) returns nvarchar(max);
GetDouble(@key <KeyType>) returns float(53);
SetDouble(@key <KeyType>, @value float(53)) returns <UDT_type>;
GetDatetime(@key <KeyType>) returns datetime;
SetDatetime(@key <KeyType>, @value datetime) returns <UDT_type>;
GetVarbinary(@key <KeyType>) returns varbinary(max);
SetVarbinary(@key <KeyType>, @value varbinary(max)) returns <UDT_type>;
SqlDecimal GetDecimal(@key <KeyType>);
SetDecimal(@key <KeyType>, @value numeric) returns <UDT_type>;
GetXml(@key <KeyType>) returns xml;
SetXml(@key <KeyType>, @value xml) returns <UDT_type>;
GetInt(@key <KeyType>) returns bigint;
SetInt(@key <KeyType>, @value bigint) returns <UDT_type>;
```

引用集合/记录的元素或为其赋值时，将使用这些方法。

```sql
-- Oracle
a_collection(i) := 'VALUE';

-- SQL Server
SET @a_collection = @a_collection.SetString(@i, 'VALUE');
```

转换具有 record 元素的多维集合或集合的赋值语句时，SSMA 会添加以下方法，以引用 set 方法中的父元素：

```sql
GetOrCreateCollectionIndexInt(@key <KeyType>) returns CollectionIndexInt;
GetOrCreateCollectionIndexString(@key <KeyType>) returns CollectionIndexString;
GetOrCreateRecord(@key <KeyType>) returns Record;
```

例如，通过以下方式创建记录元素的集合：

```sql
-- Oracle
DECLARE
    TYPE rec_details IS RECORD (id int, name varchar2(20));
    TYPE ntb1 IS TABLE of rec_details index BY binary_integer;
    c ntb1;
BEGIN
    c(1).id := 1;
END;

-- SQL Server
DECLARE
   @CollectionIndexInt$TYPE varchar(max) =
       ' TABLE INDEX BY INT OF ( RECORD ( ID INT , NAME STRING ) )',
   @c dbo.CollectionIndexInt =
       dbo.CollectionIndexInt::[Null].SetType(@CollectionIndexInt$TYPE)

SET @c = @c.SetRecord(1, @c.GetOrCreateRecord(1).SetInt(N'ID', 1))
```

## <a name="collection-built-in-methods"></a>集合内置方法

SSMA 使用以下 UDT 方法来模拟 PL/SQL 集合的内置方法。

Oracle 收集方法 | `CollectionIndexInt`和`CollectionIndexString`等效项
--- | ---
COUNT | `Count returns int`
DELETE | `RemoveAll() returns <UDT_type>`
DELETE （n） | `Remove(@index int) returns <UDT_type>`
DELETE （m，n） | `RemoveRange(@indexFrom int, @indexTo int) returns <UDT_type>`
EXISTS | `ContainsElement(@index int) returns bit`
扩展 | `Extend() returns <UDT_type>`
扩展（n） | `Extend() returns <UDT_type>`
扩展（n，i） | `ExtendDefault(@count int, @def int) returns <UDT_type>`
FIRST | `First() returns int`
LAST | `Last() returns int`
LIMIT | 空值
PRIOR | `Prior(@current int) returns int`
NEXT | `Next(@current int) returns int`
TRIM | `Trim() returns <UDT_type>`
TRIM （n） | `TrimN(@count int) returns <UDT_type>`

## <a name="bulk-collect-operation"></a>大容量收集操作

SSMA 将`BULK COLLECT INTO`语句转换为`SELECT ... FOR XML PATH` SQL Server 语句，该语句的结果包装为以下函数之一：

* `ssma_oracle.fn_bulk_collect2CollectionSimple`
* `ssma_oracle.fn_bulk_collect2CollectionComplex`

选择取决于目标对象的类型。 这些函数返回可由分析的`CollectionIndexInt`XML 值`CollectionIndexString`和`Record`类型。 特殊`AssignData`函数将基于 XML 的集合分配给 UDT。

SSMA 识别三种`BULK COLLECT INTO`语句。

### <a name="the-collection-contains-elements-with-scalar-types-and-the-select-list-contains-one-column"></a>集合包含具有标量类型的元素，且`SELECT`列表包含一列

```sql
-- Oracle
SELECT column_name_1
BULK COLLECT INTO <collection_name_1>
FROM <data_source>

-- SQL Server
SET @<collection_name_1> =
    @<collection_name_1>.AssignData(
        ssma_oracle.fn_bulk_collect2CollectionSimple(
            (SELECT column_name_1 FROM <data_source> FOR XML PATH)))
```

### <a name="the-collection-contains-elements-with-record-types-and-the-select-list-contains-one-column"></a>集合包含具有记录类型的元素，且`SELECT`列表包含一列

```sql
-- Oracle
SELECT
    column_name_1[, column_name_2...]
BULK COLLECT INTO
    <collection_name_1>
FROM
    <data_source>

-- SQL Server
SET @<collection_name_1> =
    @<collection_name_1>.AssignData(
        ssma_oracle.fn_bulk_collect2CollectionComplex(
            (SELECT
                column_name_1 as [collection_name_1_element_field_name_1],
                column_name_2 as [collection_name_1_element_field_name_2]
            FROM <data_source>
            FOR XML PATH)))
```

### <a name="the-collection-contains-elements-with-scalar-type-and-the-select-list-contains-multiple-columns"></a>该集合包含具有标量类型的元素，并且`SELECT`该列表包含多个列

```sql
-- Oracle
SELECT
    column_name_1[, column_name_2 ...]
BULK COLLECT INTO
    <collection_name_1>[, <collection_name_2> ...]
FROM
    <data_source>

-- SQL Server
;WITH bulkC AS (
    SELECT
        column_name_1 [collection_name_1_element_field_name_1],
        column_name_2 [collection_name_1_element_field_name_2]
    FROM
        <data_source>
)
SELECT
    @<collection_name_1> =
        @<collection_name_1>.AssignData(
            ssma_oracle.fn_bulk_collect2CollectionSimple(
                (SELECT
                    [collection_name_1_element_field_name_1]
                FROM
                    bulkC
                FOR XML PATH))),
    @<collection_name_2> =
        @<collection_name_2>.AssignData(
            ssma_oracle.fn_bulk_collect2CollectionSimple(
                (SELECT
                    [collection_name_1_element_field_name_2]
                FROM bulkC
                FOR XML PATH)))
```

## <a name="select-into-record"></a>选择记录

当 Oracle 查询的结果保存在 PL/SQL 记录变量中时，您有两个选项，具体取决于**将记录转换为分隔变量列表的**SSMA 设置（在 "**工具**" 菜单、"**项目设置**"、"**常规** -> **转换**" 下提供）。 如果此设置的值为 **"是"** （默认值），则 SSMA 不创建记录类型的实例。 而是通过为每个记录字段创建单独的 Transact-sql 变量，将记录拆分为构成字段。 如果设置为 "**否**"，则会实例化记录，并使用`Set`方法为每个字段分配一个值。
