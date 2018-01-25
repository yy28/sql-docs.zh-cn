---
title: "选择性 XML 索引 (SXI) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 598ecdcd-084b-4032-81b2-eed6ae9f5d44
caps.latest.revision: "9"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 82fcb8cf47767278fbc6889e49511660ef450d0c
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/19/2018
---
# <a name="selective-xml-indexes-sxi"></a>选择性 XML 索引 (SXI)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]选择性 XML 索引是除了普通 XML 索引之外可供使用的另外一种 XML 索引类型。 选择性 XML 索引功能的目标如下：  
  
-   改进对在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中存储的 XML 数据的查询性能。  
  
-   支持更快速地对较大的 XML 数据工作负荷建立索引。  
  
-   通过减少 XML 索引的存储成本提高可伸缩性。  
  
 普通 XML 索引的主要限制是要对整个 XML 文档建立索引。 这导致了主要与索引的存储成本相关的几大缺点，例如降低了查询性能和增加了索引维护成本。  
  
 通过选择性 XML 索引功能，您可以从要建立索引的 XML 文档仅提升某些路径。 在创建索引时，将对这些路径进行评估，这些路径所指向的节点将被拆分并存储于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的关系表内。 该功能采用了 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 研究院与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 产品团队合作开发的高效的映射算法。 该算法将 XML 节点映射到单个关系表，实现了不同凡响的性能且只要求有限的存储空间。  
  
 该选择性 XML 索引功能还支持针对已按选择性 XML 索引建立索引的节点的辅助选择性 XML 索引。 这些辅助选择性索引是高效的并且进一步改进了查询性能。  
  
##  <a name="benefits"></a> 选择性 XML 索引的优点  
 选择性 XML 索引具有下列优点：  
  
1.  极大改进了针对典型查询负荷的 XML 数据类型的查询性能。  
  
2.  与普通 XML 索引相比，降低了存储要求。  
  
3.  与普通 XML 索引相比，降低了索引维护成本。  
  
4.  无需更新应用程序即可享有选择性 XML 索引所带来的好处。  
  
  
##  <a name="compare"></a> 选择性 XML 索引和主 XML 索引  
  
> [!IMPORTANT]  
>  在大多数情况下，通过创建选择性 XML 索引而不是普通 XML 索引，可以改善性能和提高存储效率。  
  
 但在以下条件之一成立时，不推荐使用选择性 XML 索引：  
  
-   您要映射大量节点路径。  
  
-   您要为未知元素或文档结构内未知位置中的元素支持查询。  
  
  
##  <a name="example"></a> 选择性 XML 索引的简单示例  
 请将下面的 XML 片段视为由大约 500,000 行构成的表中的一个 XML 文档：  
  
```xml  
<book>  
    <created>2004-03-01</created>   
    <authors>Various</authors>  
    <subjects>  
        <subject>English wit and humor -- Periodicals</subject>  
        <subject>AP</subject>   
    </subjects>  
    <title>Punch, or the London Charivari, Volume 156, April 2, 1919</title>  
    <id>etext11617</id>  
</book>  
```  
  
 对由这么多行构成的这个简单架构创建主 XML 索引会用较长的时间。 对此数据进行查询还面临这样一个问题，即主 XML 索引不支持选择性索引。  
  
 如果您仅需要对 `/book/title` 路径和 `/book/subjects` 路径查询此数据，则可以创建以下选择性 XML 索引：  
  
```sql  
CREATE SELECTIVE XML INDEX SXI_index  
ON Tbl(xmlcol)  
FOR   
(  
    pathTitle = '/book/title/text()' AS XQUERY 'xs:string',   
    pathAuthors = '/book/authors' AS XQUERY 'node()',  
    pathId = '/book/id' AS SQL NVARCHAR(100)  
)  
```  
  
 前面的语句是您在创建选择性 XML 索引时使用的 CREATE 语法的一个很好的例子。 在 CREATE 语句中，您首先为索引提供名称，并且标识要建立索引的表和 XML 列。 然后，您提供要建立索引的路径。 一个路径由三个部分构成：  
  
1.  唯一标识该路径的名称。  
  
2.  描述该路径的 XQuery 表达式。  
  
3.  可选的优化提示。  
  
 有关这些元素的详细信息，请参阅 [相关任务](#reltasks)。  
  
  
## <a name="supported-features-prerequisites-and-limitations"></a>支持的功能、先决条件和限制  
  
###  <a name="features"></a> 支持的 XML 功能  
 选择性 XML 索引在 exist()、value() 和 nodes() 方法内支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所支持的 XQuery。  
  
-   对于 exist()、value() 和 nodes() 方法，选择性 XML 索引包含用于转换整个表达式的足够信息。  
  
-   对于 query() 和 modify() 方法，选择性 XML 索引只能用于节点筛选。  
  
-   对于 query() 方法，选择性 XML 索引不用于检索结果。  
  
-   对于 modify() 方法，选择性 XML 索引不用于更新 XML 文档。  
  
  
###  <a name="unsupported"></a> 不支持的 XML 功能  
 选择性 XML 索引不支持在 XML 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实现中支持的以下功能：  
  
-   对具有复杂 XS 类型的节点建立索引：联合类型、序列类型和列表类型。  
  
-   对具有二进制 XS 类型的节点建立索引：例如 base64Binary 和 hexBinary。  
  
-   使用在末尾包含通配符 `*` 的 XPath 表达式指定要建立索引的节点：例如  `/a/b/c/*`、 `/a//b/*`或 `/a/b/*:c`。  
  
-   对子级、属性或后代以外的任何轴建立索引。 `//<step>` 的情况允许作为特例。  
  
-   对 XML 处理指令和注释建立索引。  
  
-   通过使用 id() 函数为节点指定和检索标识符。  
  
  
###  <a name="prereq"></a> 先决条件  
 必须首先满足以下先决条件，然后才能对用户表中的 XML 列创建选择性 XML 索引：  
  
-   聚集索引必须存在于用户表的主键上。  
  
-   在用于选择性 XML 索引时，用户表的主键限制为 128 字节大小。  
  
-   在用于选择性 XML 索引时，用户表的聚集键限制为 15 列。  
  
  
###  <a name="limits"></a> 限制  
 **一般要求和限制**  
  
-   只能对单个 XML 列创建各个选择性 XML 索引。  
  
-   不能对非 XML 列创建选择性 XML 索引。  
  
-   表中的每个 XML 列只能具有一个选择性 XML 索引。  
  
-   每个表最多可具有 249 个选择性 XML 索引。  
  
 **对支持的对象的限制**  
  
 不能对以下对象创建选择性 XML 索引：  
  
1.  视图中的 XML 列。  
  
2.  具有 XML 列的表值变量。  
  
3.  XML 类型变量。  
  
4.  计算出的 XML 列。  
  
5.  深度超过 128 个嵌套节点的 XML 列。  
  
 **与存储相关的限制**  
  
 对于可添加到索引中的 XML 文档中的节点数有一定的限制。 选择性 XML 索引将 XML 文档映射到单个关系表。 因此，在表的任何给定行中，选择性 XML 索引不能具有超过 1024 个非 Null 列。 此外，针对稀疏列的许多限制也适用于选择性 XML 索引，因为这些索引使用稀疏列来进行存储。  
  
 在任何给定行中支持的非 Null 列的最大数目依赖于列中的数据大小：  
  
-   在最佳情形下，在所有列的类型均为 **bit**时支持 1024 个非 Null 列。  
  
-   在最差情形下，在所有列均为 **varchar**类型的大型对象时仅支持 236 个非 Null 列。  
  
 选择性 XML 索引为建立索引的每个节点路径在内部使用一到四个列。 可建立索引的节点总数从 60 个节点到几百个节点不等，具体数目取决于已建立索引的路径中数据的实际大小。  
  
-   在最差情形下，在节点路径定义中使用 `//` 映射某些或所有节点时，已建立索引的节点的最大数目是 60。  
  
-   在最佳情形下，在节点路径定义中未使用 `//` 映射节点时，已建立索引的节点的最大数目是 200。  
  
 **在您使用 CREATE 或 ALTER 语句对索引执行操作时，将重新生成选择性 XML 索引。**  
  
 在您使用 CREATE 或 ALTER 语句对选择性 XML 索引执行操作时，将在单线程的脱机模式下重新生成该索引。 频繁使用 ALTER 语句会对针对已建立索引的 XML 文档执行的查询的性能造成负面影响。  
  
 **其他限制**  
  
-   在查询提示中不支持选择性 XML 索引。  
  
-   在数据库优化顾问中不支持选择性 XML 索引和辅助选择性 XML 索引。  
  
  
##  <a name="reltasks"></a> 相关任务  
  
|||  
|-|-|  
|**任务**|**主题**|  
|在创建或更改选择性 XML 索引时，指定要建立索引的节点路径以及可选的优化提示。|[为选择性 XML 索引指定路径和优化提示](../../relational-databases/xml/specify-paths-and-optimization-hints-for-selective-xml-indexes.md)|  
|创建、更改或删除选择性 XML 索引。|[创建、更改和删除选择性 XML 索引](../../relational-databases/xml/create-alter-and-drop-selective-xml-indexes.md)|  
|创建、更改或删除辅助选择性 XML 索引。|[创建、更改和删除辅助选择性 XML 索引](../../relational-databases/xml/create-alter-and-drop-secondary-selective-xml-indexes.md)|  
  
  
  
