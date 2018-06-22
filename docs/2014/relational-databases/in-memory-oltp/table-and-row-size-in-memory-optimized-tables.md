---
title: 内存优化表中的表和行大小 | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b0a248a4-4488-4cc8-89fc-46906a8c24a1
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: 5c35ff979ce6d5e37d8eaba1942da681d3a73470
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015684"
---
# <a name="table-and-row-size-in-memory-optimized-tables"></a>内存优化表中的表和行大小
  内存优化表由行和索引的集合组成，其中包含行的指针。 在一个内存优化表中，行不能长于 8,060 字节。 了解内存优化表的大小将帮助您了解计算机是否具有足够的内存。  
  
 有两个原因要计算表和行大小：  
  
-   一个表使用多少内存？  
  
    -   表使用的内存量无法精确计算。 有很多因素影响使用的内存量。 例如基于页的内存分配、位置、缓存和填充等因素。 还有具有活动事务关联或等待垃圾收集的多个行版本。  
  
    -   表中数据和索引所需的最小大小由下面讨论的 [表大小] 计算给定。  
  
    -   计算内存使用量最好也不过是个近似值，建议您将容量规划包含在部署计划中。  
  
-   行的数据大小是多少，是否满足 8,060 字节行大小限制？ 要回答这些问题，需要使用下面讨论的 [行正文大小] 计算。  
  
 下图是一个包含索引和行的表，因而也就有行标题和正文：  
  
 ![内存优化表。](../../database-engine/media/hekaton-guide-1.gif "Memory optimized table.")  
内存优化表，由索引和行组成。  
  
 内存中的表大小（以字节为单位）计算如下：  
  
```  
[table size] = [size of index 1] + … + [size of index n] + ([row size] * [row count])  
```  
  
 哈希索引的大小是在表创建时固定下来的，取决于实际 Bucket 计数。 用索引规范指定的 bucket_count 舍入为最近的 2 次幂以获取 [实际 Bucket 计数]。 例如，如果指定的 bucket_count 为 100000，则索引的 [实际 Bucket 计数] 为 131072。  
  
```  
[hash index size] = 8 * [actual bucket count]  
```  
  
 行大小是通过添加标题和正文计算的：  
  
```  
[row size] = [row header size] + [actual row body size]  
[row header size] = 24 + 8 * [number of indices]  
```  
  
 **行正文大小**  
  
 [行正文大小] 的计算在下表中讨论。  
  
 对于行正文大小，有两种不同的计算：计算大小和实际大小。  
  
-   计算大小表示为 [计算行正文大小]，用于确定是否超出了 8,060 字节的行大小限制。  
  
-   实际大小表示为 [实际行正文大小]，是行正文在内存和检查点文件中的实际存储大小。  
  
 [计算行正文大小] 和 [实际行正文大小] 的计算方式相似。 唯一的区别是 (n)varchar(i) 和 varbinary(i) 列大小的计算，如下表底部所示。 计算行正文大小使用声明的大小 *i* 作为列大小，而实际行正文大小使用实际数据大小。  
  
 下表介绍行正文大小的计算，公式为 [实际行正文大小] = SUM([浅表类型的大小]) + 2 + 2 * [深表类型列数]。  
  
|部分|Size|注释|  
|-------------|----------|--------------|  
|浅表类型列|SUM([浅表类型的大小])<br /><br /> **各类型的大小是，如下所示：**<br /><br /> Bit &#124; 1<br /><br /> Tinyint &#124; 1<br /><br /> Smallint &#124; 2<br /><br /> Int &#124; 4<br /><br /> Real &#124; 4<br /><br /> Smalldatetime &#124; 4<br /><br /> Smallmoney &#124; 4<br /><br /> Bigint &#124; 8<br /><br /> Datetime &#124; 8<br /><br /> Datetime2 &#124; 8<br /><br /> Float 8<br /><br /> Money 8<br /><br /> 数字 (精度 < = 18) &#124; 8<br /><br /> Time &#124; 8<br /><br /> Numeric(precision>18) &#124; 16<br /><br /> Uniqueidentifier &#124; 16||  
|浅表列填充|可能的值有：<br /><br /> 如果存在深表类型列并且浅表列的总数据大小是奇数，则为 1。<br /><br /> 否则为 0|深表类型为类型 (var)binary 和 (n)(var)char。|  
|深表类型列的偏移数组|可能的值有：<br /><br /> 如果没有深表类型列，则为 0<br /><br /> 否则为 2 + 2 * [深表类型列数]|深表类型为类型 (var)binary 和 (n)(var)char。|  
|NULL 数组|[可以为 Null 的列数] / 8，舍入为完整字节。|数组每个可以为 Null 的列有一位。 这舍入为完整字节。|  
|NULL 数组填充|可能的值有：<br /><br /> 如果存在深表类型列并且 NULL 数组的大小为奇数字节，则为 1。<br /><br /> 否则为 0|深表类型为类型 (var)binary 和 (n)(var)char。|  
|填充|如果没有深表类型列，则为 0<br /><br /> 如果有深表类型列，则根据浅表列需要的最大对齐添加 0-7 个填充字节。 每个浅表列都需要与上述大小相等的对齐，而 GUID 列需要 1（而不是 16）字节的对齐，数值列始终需要 8（而不是 16）字节的对齐。 所有浅表列间使用最大的对齐要求，添加了 0-7 个字节，现在总大小（不带深表类型列）是所需对齐的数倍。|深表类型为类型 (var)binary 和 (n)(var)char。|  
|固定长度的深表类型列|SUM([固定长度深表类型列的大小])<br /><br /> 各列大小如下：<br /><br /> 对于 char(i) 和 binary(i)，为 i。<br /><br /> 对于 nchar(i)，为 2 * i|固定长度深表类型列是类型为 char(i)、nchar(i) 或 binary(i) 的列。|  
|可变长度深表类型列 [计算大小]|SUM([可变长度深表类型列的计算大小])<br /><br /> 各列的计算大小如下：<br /><br /> 对于 varchar(i) 和 varbinary(i)，为 i<br /><br /> 对于 nvarchar(i)，为 2 * i|此行仅适用于 [计算行正文大小]。<br /><br /> 可变长度的深表类型列是类型为 varchar(i)、nvarchar(i) 或 varbinary(i) 的列。 计算大小由列的最大长度 (i) 决定。|  
|可变长度深表类型列 [实际大小]|SUM([可变长度深表类型列的实际大小])<br /><br /> 各列的实际大小如下：<br /><br /> 对于 varchar(i) 为 n，其中 n 是列中存储的字符数。<br /><br /> 对于 nvarchar(i) 为 2 * n，其中 n 是列中存储的字符数。<br /><br /> 对于 varbinary(i) 为 n，其中 n 是列中存储的字节数。|此行仅适用于 [实际行正文大小]。<br /><br /> 实际大小由相应行中各列存储的数据决定。|  
  
##  <a name="bkmk_RowStructure"></a> 行结构  
 内存优化表中的行包含以下组成部分：  
  
-   行标题，包含实现行版本控制所必需的时间戳。 此外，行标题还包含索引指针，以实现哈希 Bucket 中的行链（如上所述）。  
  
-   行正文，包含实际的列数据，其中包括一些辅助信息，如用于可为 Null 的列的 Null 数组，用于变长数据类型的偏移数组等。  
  
 下图展示拥有两个索引的表的行结构：  
  
 ![具有两个索引的表的行结构。](../../database-engine/media/hekaton-tables-4.gif "具有两个索引的表的行结构。")  
  
 开始和结束时间戳指示特定行版本的有效时长。 在该时间间隔启动的事务可看到该行版本。 有关更多详细信息，请参阅[内存优化表中的事务](memory-optimized-tables.md)。  
  
 索引指针，指向链中属于该哈希 Bucket 的下行。 下图展示一个表结构，其拥有两列（姓名，城市）、两个索引（一个针对姓名列、一个针对城市列）。  
  
 ![具有两个列和索引的表的结构。](../../database-engine/media/hekaton-tables-5.gif "具有两个列和索引的表的结构。")  
  
 在该图中，姓名 John 和 Jane 经哈希处理放入第一个 Bucket。 Susan 经哈希处理放入第二个 Bucket。 城市 Beijing 和 Bogota 经哈希处理放入第一个 Bucket。 Paris 和 Prague 经哈希处理放入第二个 Bucket。  
  
 因此，针对姓名的哈希索引的链如下所示：  
  
-   第一个 Bucket：(John, Beijing); (John, Paris); (Jane, Prague)  
  
-   第二个 Bucket：(Susan, Bogota)  
  
 针对城市的索引的链如下所示：  
  
-   第一个 Bucket：(John, Beijing), (Susan, Bogota)  
  
-   第二个 Bucket：(John, Paris), (Jane, Prague)  
  
 结束时间戳 ∞（无限制）指示此为当前有效的行版本。 该行自该行版本写入以来尚未更新或删除。  
  
 对于大于 200 的时间，该表包含以下行：  
  
|“属性”|City|  
|----------|----------|  
|John|Beijing|  
|Jane|Prague|  
  
 但是，开始时间为 100 的任意活动事务都将看到该表的以下版本：  
  
|“属性”|City|  
|----------|----------|  
|John|Paris|  
|Jane|Prague|  
|Susan|Bogata|  
  
##  <a name="bkmk_ExampleComputation"></a> 示例：表和行大小计算  
 对于哈希索引，实际 Bucket 计数舍入为最近的 2 次幂。 例如，如果指定的 bucket_count 为 100000，则索引的实际 Bucket 计数为 131072。  
  
 考虑具有以下定义的 Orders 表：  
  
```tsql  
CREATE TABLE dbo.Orders (  
     OrderID int NOT NULL   
           PRIMARY KEY NONCLUSTERED,  
     CustomerID int NOT NULL   
           INDEX IX_CustomerID HASH WITH (BUCKET_COUNT=10000),  
     OrderDate datetime NOT NULL,  
     OrderDescription nvarchar(1000)  
) WITH (MEMORY_OPTIMIZED=ON)  
GO  
```  
  
 请注意，此表有一个哈希索引和一个非聚集索引（主键）。 它还有三个固定长度列和一个可变长度列，其中一列可以为 NULL (OrderDescription)。 我们假定 Orders 表有 8379 行，OrderDescription 列值的平均长度为 78 个字符。  
  
 要确定表大小，首先需要确定索引大小。 两个索引的 bucket_count 都指定为 10000。 这舍入为最近的 2 次幂：16384。 因此，Orders 表的索引的总大小为：  
  
```  
8 * 16384 = 131072 bytes  
```  
  
 其余为表数据大小，即  
  
```  
[row size] * [row count] = [row size] * 8379  
```  
  
 （示例表有 8379 行。）现在：  
  
```  
[row size] = [row header size] + [actual row body size]  
[row header size] = 24 + 8 * [number of indices] = 24 + 8 * 1 = 32 bytes  
```  
  
 接下来，我们计算 [实际行正文大小]：  
  
-   浅表类型列：  
  
    ```  
    SUM([size of shallow types]) = 4 [int] + 4 [int] + 8 [datetime] = 16  
    ```  
  
-   因为总浅表列大小为偶数，所以浅表列填充为 0。  
  
-   深表类型列的偏移数组：  
  
    ```  
    2 + 2 * [number of deep type columns] = 2 + 2 * 1 = 4  
    ```  
  
-   NULL 数组 = 1  
  
-   Null 数组填充 = 1，因为 Null 数组大小为奇数并且有深表类型列。  
  
-   填充  
  
    -   8 是最大对齐要求。  
  
    -   目前大小为 16 + 0 + 4 + 1 + 1 = 22。  
  
    -   最接近的 8 的倍数为 24。  
  
    -   总填充为 24 – 22 = 2 字节。  
  
-   没有固定长度深表类型列（固定长度深表类型列：0）。  
  
-   深表类型列的实际大小为 2 * 78 = 156。 唯一的深表类型列 OrderDescription 的类型为 nvarchar。  
  
```  
[actual row body size] = 24 + 156 = 180 bytes  
```  
  
 完成计算：  
  
```  
[row size] = 32 + 180 = 212 bytes  
[table size] = 8 * 16384 + 212 * 8379 = 131072 + 1776348 = 1907420  
```  
  
 内存中的总表大小约为 2 MB。 这不包括内存分配引起的可能开销以及访问此表的事务所需的行版本控制引起的可能开销。  
  
 实际分配的内存和此表及其索引使用的内存可以通过以下查询获得：  
  
```tsql  
select * from sys.dm_db_xtp_table_memory_stats  
where object_id = object_id('dbo.Orders')  
```  
  
## <a name="see-also"></a>请参阅  
 [内存优化表](memory-optimized-tables.md)  
  
  