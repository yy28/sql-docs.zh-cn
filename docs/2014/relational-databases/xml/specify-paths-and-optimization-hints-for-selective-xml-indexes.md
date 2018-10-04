---
title: 为选择性 XML 索引指定路径和优化提示 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
ms.assetid: 486ee339-165b-4aeb-b760-d2ba023d7d0a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 73cfcc602ee7a7ef273da39126dbd4da596b6594
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48133517"
---
# <a name="specify-paths-and-optimization-hints-for-selective-xml-indexes"></a>为选择性 XML 索引指定路径和优化提示
  本主题介绍如何在创建或更改选择性 XML 索引时，如何指定要建立索引的节点路径以及用于索引的优化提示。  
  
 您可以在以下语句之一中同时指定节点路径和优化提示：  
  
-   在 **CREATE** 语句的 **FOR** 子句中。 有关详细信息，请参阅 [CREATE SELECTIVE XML INDEX (Transact-SQL)](/sql/t-sql/statements/create-selective-xml-index-transact-sql)。  
  
-   在 **ALTER** 语句的 **ADD** 子句中。 有关详细信息，请参阅 [ALTER INDEX（选择性 XML 索引）](../indexes/indexes.md)。  
  
 有关选择性 XML 索引的详细信息，请参阅 [选择性 XML 索引 (SXI)](../xml/selective-xml-indexes-sxi.md)。  
  
##  <a name="untyped"></a> 了解非类型化 XML 中的 XQuery 和 SQL Server 类型  
 选择性 XML 索引支持两种类型系统：XQuery 类型和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 类型。 已建立索引的路径可用于匹配 XQuery 表达式，或者用于匹配 XML 数据类型的 value() 方法的返回值。  
  
-   在未对要建立索引的路径加批注时，或者使用 XQUERY 关键字进行批注时，该路径匹配 XQuery 表达式。 对于 XQUERY 批注的节点路径有两种变化形式：  
  
    -   如果没有指定 XQUERY 关键字和 XQuery 数据类型，则使用默认映射。 通常，性能和存储并非最佳。  
  
    -   如果指定 XQUERY 关键字和 XQuery 数据类型以及可选的其他优化提示，则您可以实现可能最佳的性能以及可能最高效的存储。 但是，转换可能会失败。  
  
-   在使用 SQL 关键字对要建立索引的路径加批注时，该路径匹配 XML 数据类型的 value() 方法的返回值。 指定相应的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型，该数据类型是预期从 value() 方法的返回类型。  
  
 在应用于 XML 数据类型的 value() 方法的 XQuery 表达式 XML 类型系统和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 类型系统之间存在细微的差异。 这些差异如下：  
  
-   XQuery 类型系统知道尾随空格。 例如，根据 XQuery 类型语义，字符串“abc”和“abc ”不相等；而在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，这两个字符串是相等的。  
  
-   XQuery 浮点数据类型支持 +/- 零和 +/- 无穷大的特殊值。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 浮点数据类型中不支持这些特殊值。  
  
### <a name="xquery-types-in-untyped-xml"></a>非类型化 XML 中的 XQuery 类型  
  
-   XQuery 类型匹配 XML 数据类型的所有方法（包括 value() 方法）中的 XQuery 表达式。  
  
-   XQuery 类型支持以下优化提示：node()、SINGLETON、DATA TYPE 和 MAXLENGTH。  
  
 对于针对非类型化 XML 的 XQuery 表达式，您可以在以下两个操作模式之间进行选择：  
  
-   **默认的映射模式**。 在这个模式中，您在创建选择性 XML 索引时仅指定路径。  
  
-   **用户指定的映射模式**。 在这个模式中，您既指定路径，也指定可选的优化提示。  
  
 默认映射模式使用一个保守的存储选项，这个选项始终是安全和一般性的。 该模式可以匹配任何表达式类型。 默认映射模式的一个限制就是逊色于最佳性能，因为需要增加运行时转换的数目，并且辅助索引不可用。  
  
 下面是使用默认映射创建的一个选择性 XML 索引的示例。 对于所有三个路径，使用默认节点类型 (**xs:untypedAtomic**) 和基数。  
  
```tsql  
CREATE SELECTIVE XML INDEX example_sxi_UX_default  
ON Tbl(xmlcol)  
FOR  
(  
mypath01 =  '/a/b',  
mypath02 = '/a/b/c',  
mypath03 = '/a/b/d'  
)  
```  
  
 通过用户指定的映射模式，您可以为节点指定类型和基数以便实现更好的性能。 但是，这一性能的提升是通过放弃安全性（因为转换可能会失败）和一般性（因为只有指定的类型与选择性 XML 索引匹配）来实现的。  
  
 支持非类型化 XML 事例的 XQuery 类型包括：  
  
-   **xs:boolean**  
  
-   **xs:double**  
  
-   **xs:string**  
  
-   **xs:date**  
  
-   **xs:time**  
  
-   **xs:dateTime**  
  
 如果未指定该类型，则认为节点属于 **xs:untypedAtomic** 数据类型。  
  
 您可以优化以下方式中所示的选择性 XML 索引：  
  
```tsql  
CREATE SELECTIVE XML INDEX example_sxi_UX_optimized  
ON Tbl(xmlcol)  
FOR  
(  
mypath= '/a/b' as XQUERY 'node()',  
pathX = '/a/b/c' as XQUERY 'xs:double' SINGLETON,  
pathY = '/a/b/d' as XQUERY 'xs:string' MAXLENGTH(200) SINGLETON  
)  
-- mypath – Only the node value is needed; storage is saved.  
-- pathX – Performance is improved; secondary indexes are possible.  
-- pathY - Performance is improved; secondary indexes are possible; storage is saved.  
```  
  
### <a name="sql-server-types-in-untyped-xml"></a>非类型化 XML 中的 SQL Server 类型  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 类型匹配 value() 方法的返回值。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 类型支持此优化提示：SINGLETON。  
  
 对于返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 类型的路径，必须指定某一类型。 使用您要在 value() 方法中使用的相同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 类型。  
  
 请考虑以下查询：  
  
```tsql  
SELECT T.record,  
    T.xmldata.value('(/a/b/d)[1]', 'NVARCHAR(200)')  
FROM myXMLTable T  
```  
  
 该指定的查询从打包到 NVARCHAR(200) 数据类型中的路径 `/a/b/d` 返回一个值，因此，要为该节点指定的数据类型十分明显。 但是，没有用于在非类型化 XML 中指定节点基数的架构。 若要指定节点 `d` 在其父节点 `b`下最多出现一次，请创建一个选择性 XML 索引，该索引使用 SINGLETON 优化提示，如下所示：  
  
```tsql  
CREATE SELECTIVE XML INDEX example_sxi_US  
ON Tbl(xmlcol)  
FOR  
(  
node1223 = '/a/b/d' as SQL NVARCHAR(200) SINGLETON  
)  
```  
  

  
##  <a name="typed"></a> 了解对类型化 XML 的选择性 XML 索引支持  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的类型化 XML 是与某一给定 XML 文档相关联的架构。 该架构定义文档的整体结构以及节点的类型。 如果某一架构存在，则在用户提升路径时选择性 XML 索引将应用该架构结构，因此，无需为路径指定 XQUERY 类型。  
  
 选择性 XML 索引支持以下 XSD 类型：  
  
-   **xs:anyUri**  
  
-   **xs:boolean**  
  
-   **xs:date**  
  
-   **xs:dateTime**  
  
-   **xs:day**  
  
-   **xs:decimal**  
  
-   **xs:double**  
  
-   **xs:float**  
  
-   **xs:int**  
  
-   **xs:integer**  
  
-   **xs:language**  
  
-   **xs:long**  
  
-   **xs:name**  
  
-   **xs:NCName**  
  
-   **xs:negativeInteger**  
  
-   **xs:nmtoken**  
  
-   **xs:nonNegativeInteger**  
  
-   **xs:nonPositiveInteger**  
  
-   **xs:positiveInteger**  
  
-   **xs:qname**  
  
-   **xs:short**  
  
-   **xs:string**  
  
-   **xs:time**  
  
-   **xs:token**  
  
-   **xs:unsignedByte**  
  
-   **xs:unsignedInt**  
  
-   **xs:unsignedLong**  
  
-   **xs:unsignedShort**  
  
 在对具有与其相关联的架构的文档创建选择性 XML 索引时，在创建或更改索引时指定 XQUERY 类型会返回错误。 用户可以在路径提升部分中使用 SQL 类型批注。 该 SQL 类型必须是从该架构中定义的 XSD 类型的有效转换，否则将引发错误。 支持在 XSD 中具有足够的表示形式的几乎所有 SQL 类型，只有日期/时间类型除外。  
  
> [!NOTE]  
>  如果在选择性 XML 索引路径提升中指定的类型与 value() 方法返回值相同，则使用选择性索引。  
  
 下面的优化提示可用于类型化 XML 文档：  
  
-   node() 优化提示。  
  
-   MAXLENGTH 优化提示可用于 xs:string 类型，以便缩短索引值。  
  
 有关优化提示的详细信息，请参阅 [指定优化提示](#hints)。  
  
##  <a name="paths"></a> 指定路径  
 通过选择性 XML 索引，您可以从您预期要运行的查询相关的已存储 XML 数据仅对节点的子集建立索引。 在相关节点的子集远小于 XML 文档中节点的总数时，选择性 XML 索引将仅存储相关节点。 为了从选择性 XML 索引中受益，请标识要建立索引的正确的节点子集。  
  
### <a name="choosing-the-nodes-to-index"></a>选择要建立索引的节点  
 您可以使用以下两个简单的原则来标识要添加到选择性 XML 索引的正确的节点子集。  
  
1.  **原则 1**：若要评估某一给定的 XQuery 表达式，请对需要检查的所有节点建立索引。  
  
    -   对其本身或值用于 XQuery 表达式中的所有节点建立索引。  
  
    -   对应用了 XQuery 谓词的 XQuery 表达式中的所有节点建立索引。  
  
     请考虑以下简单查询，它针对本文中的 [示例 XML 文档](#sample) ：  
  
    ```tsql  
    SELECT T.record FROM myXMLTable T  
    WHERE T.xmldata.exist('/a/b[./c = "43"]') = 1  
    ```  
  
     为了返回满足此查询的 XML 实例，选择性 XML 索引需要在每个 XML 实例中都检查两个节点：  
  
    -   节点 `c`，因为其值用于 XQuery 表达式中。  
  
    -   节点 `b`，因为在 XQuery 表达式中一个谓词应用于节点`b` 。  
  
2.  **原则 2**：为了得到最佳性能，为对某一给定 XQuery 表达式进行求值所需的所有节点建立索引。 如果您仅对其中某些节点建立索引，则选择性 XML 索引将改进只包含已建立索引的节点的子表达式的求值。  
  
 为了提高上面所示的 SELECT 语句的性能，您可以创建以下选择性 XML 索引：  
  
```tsql  
CREATE SELECTIVE XML INDEX simple_sxi  
ON Tbl(xmlcol)  
FOR  
(  
    path123 =  '/a/b',  
    path124 =  '/a/b/c'  
)  
```  
  
### <a name="indexing-identical-paths"></a>对完全相同的路径建立索引  
 您不能将基于不同路径名称的完全相同的路径提升为相同的数据类型。 例如，以下查询将会引发错误，因为 `pathOne` 和 `pathTwo` 完全相同：  
  
```tsql  
CREATE SELECTIVE INDEX test_simple_sxi ON T1(xmlCol)  
FOR  
(  
    pathOne = 'book/authors/authorID' AS XQUERY 'xs:string',  
    pathTwo = 'book/authors/authorID' AS XQUERY 'xs:string'  
)  
```  
  
 但是，您可以将完全相同的路径提升为具有不同名称的不同数据类型。 例如，下面的查询现在是可接受的，因为数据类型不同：  
  
```tsql  
CREATE SELECTIVE INDEX test_simple_sxi ON T1(xmlCol)  
FOR  
(  
    pathOne = 'book/authors/authorID' AS XQUERY 'xs:double',  
    pathTwo = 'book/authors/authorID' AS XQUERY 'xs:string'  
)  
```  
  
### <a name="examples"></a>示例  
 下面是其他一些示例，说明如何为不同的 XQuery 类型选择要建立索引的正确节点。  
  
 **示例 1**  
  
 下面是使用 exist() 方法的一个简单的 XQuery：  
  
```tsql  
SELECT T.record FROM myXMLTable T  
WHERE T.xmldata.exist('/a/b/c/d/e/h') = 1  
```  
  
 下表显示应建立索引以便让此查询使用选择性 XML 索引的节点。  
  
|要包含在索引中的节点|为此节点建立索引的原因|  
|----------------------------------|-----------------------------------|  
|**/a/b/c/d/e/h**|在 exist() 方法中为存在的节点 `h` 进行求值。|  
  
 **示例 2**  
  
 下面是应用了谓词的前面的 XQuery 的更复杂变化形式：  
  
```tsql  
SELECT T.record FROM myXMLTable T  
WHERE T.xmldata.exist('/a/b/c/d/e[./f = "SQL"]') = 1  
```  
  
 下表显示应建立索引以便让此查询使用选择性 XML 索引的节点。  
  
|要包含在索引中的节点|为此节点建立索引的原因|  
|----------------------------------|-----------------------------------|  
|**/a/b/c/d/e**|一个谓词应用于节点 `e`。|  
|**/a/b/c/d/e/f**|在该谓词内对节点 `f` 的值进行求值。|  
  
 **示例 3**  
  
 下面是具有 value() 子句的更复杂查询：  
  
```tsql  
SELECT T.record,  
    T.xmldata.value('(/a/b/c/d/e[./f = "SQL"]/g)[1]', 'nvarchar(100)')  
FROM myXMLTable T  
```  
  
 下表显示应建立索引以便让此查询使用选择性 XML 索引的节点。  
  
|要包含在索引中的节点|为此节点建立索引的原因|  
|----------------------------------|-----------------------------------|  
|**/a/b/c/d/e**|一个谓词应用于节点 `e`。|  
|**/a/b/c/d/e/f**|在该谓词内对节点 `f` 的值进行求值。|  
|**/a/b/c/d/e/g**|value() 方法返回节点 `g` 的值。|  
  
 **示例 4**  
  
 下面是在 exist() 子句内使用 FLWOR 子句的查询。 （FLWOR 这个名称来自于可构成一个 XQuery FLWOR 表达式的五个子句：for、let、where、order by 和 return。）  
  
```tsql  
SELECT T.record FROM myXMLTable T  
WHERE T.xmldata.exist('  
  For $x in /a/b/c/d/e  
  Where $x/f = "SQL"  
  Return $x/g  
') = 1  
```  
  
 下表显示应建立索引以便让此查询使用选择性 XML 索引的节点。  
  
|要包含在索引中的节点|为此节点建立索引的原因|  
|----------------------------------|-----------------------------------|  
|**/a/b/c/d/e**|在 FLWOR 子句中为存在的节点 `e` 进行求值。|  
|**/a/b/c/d/e/f**|在 FLWOR 子句中为节点 `f` 的值进行求值。|  
|**/a/b/c/d/e/g**|通过 exist() 方法为存在的节点 `g` 进行求值。|  
  

  
##  <a name="hints"></a> 指定优化提示  
 您可以使用可选的优化提示为按选择性 XML 索引建立索引的节点指定附加的映射详细信息。 例如，可以指定节点的数据类型和基数，以及与数据结构有关的某些信息。 这些附加信息支持更好的映射。 它还可以导致改进性能和/或节约存储空间。  
  
 是否使用优化提示是可选的。 您可以始终接受默认映射，这样做是可靠的，但无法提供最佳性能和存储。  
  
 某些优化提示（例如 SINGLETON 提示）会引入针对您的数据的约束。 在某些情况下，在未满足这些约束时可能会引发错误。  
  
### <a name="benefits-of-optimization-hints"></a>优化提示的好处  
 下表标识支持更高效的存储或改进的性能的优化提示。  
  
|优化提示|更高效的存储|改进的性能|  
|-----------------------|----------------------------|--------------------------|  
|**node()**|用户帐户控制|否|  
|**SINGLETON**|否|用户帐户控制|  
|**DATA TYPE**|用户帐户控制|用户帐户控制|  
|**MAXLENGTH**|用户帐户控制|用户帐户控制|  
  
### <a name="optimization-hints-and-data-types"></a>优化提示和数据类型  
 您可以将节点作为 XQuery 数据类型或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型建立索引。 下表显示了每种数据类型支持的优化提示。  
  
|优化提示|XQuery 数据类型|SQL 数据类型|  
|-----------------------|-----------------------|--------------------|  
|**node()**|用户帐户控制|否|  
|**SINGLETON**|用户帐户控制|用户帐户控制|  
|**DATA TYPE**|用户帐户控制|否|  
|**MAXLENGTH**|用户帐户控制|否|  
  
### <a name="node-optimization-hint"></a>node() 优化提示  
 适用于：XQuery 数据类型  
  
 您可以使用 node() 优化指定其值无需用于对典型查询进行求值的节点。 在典型查询仅需要为存在的节点进行求值时，此提示可降低存储要求。 （默认情况下，选择性 XML 查询将存储几乎所有提升的节点的值，只有复杂节点类型除外。）  
  
 请参考如下示例：  
  
```tsql  
SELECT T.record FROM myXMLTable T  
WHERE T.xmldata.exist('/a/b[./c=5]') = 1  
```  
  
 若要使用选择性 XML 索引对此查询进行求值，请提升节点 `b` 和 `c`。 但是，因为节点 `b` 的值不是必需的，所以，您可以将 node() 提示用于以下语法：  
  
 `/a/b/ as node()`  
  
 如果某个查询要求已使用 node() 提示建立索引的节点值，则不能使用选择性 XML 索引。  
  
### <a name="singleton-optimization-hint"></a>SINGLETON 优化提示  
 适用于：XQuery 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型  
  
 SINGLETON 优化提示指定节点的基数。 此提示将改进查询性能，因为提前知道节点在其父节点或祖先节点内最多出现一次。  
  
 请考虑本主题中的 [示例 XML 文档](#sample) 。  
  
 若要使用选择性 XML 索引对此文档进行查询，您可为节点 `d` 指定 SINGLETON 提示，因为该节点在其父节点内最多出现一次。  
  
 如果已指定 SINGLETON 提示，但某一节点在其父节点或祖先节点内出现多次，则在您创建索引（为现有数据）或运行查询（为新数据）时将引发错误。  
  
### <a name="data-type-optimization-hint"></a>DATA TYPE 优化提示  
 适用于：XQuery 数据类型  
  
 通过 DATA TYPE 优化提示，您可以为已建立索引的节点指定 XQuery 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型。 该数据类型用于与选择性 XML 索引的数据表中与已建立索引的节点相对应的列。  
  
 在将现有值转换为指定的数据类型失败时，插入操作（插入到索引中）不会失败；但是，一个 null 值将插入到索引的数据表中。  
  
### <a name="maxlength-optimization-hint"></a>MAXLENGTH 优化提示  
 适用于：XQuery 数据类型  
  
 通过 MAXLENGTH 优化提示，您可以限制 xs:string 数据的长度。 MAXLENGTH 与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型不相关，因为您在指定 VARCHAR 或 NVARCHAR 日期类型时指定长度。  
  
 在现有字符串长于指定的 MAXLENGTH 时，将该值插入到索引中将失败。  
  

  
##  <a name="sample"></a> 针对示例的示例 XML 文档  
 下面的示例 XML 文档在本主题的示例中引用：  
  
```xml  
<a>  
    <b>  
         <c atc="aa">10</c>  
         <c atc="bb">15</c>  
         <d atd1="dd" atd2="ddd">md </d>  
    </b>  
     <b>  
        <c></c>  
        <c atc="">117</c>  
     </b>  
</a>  
```  
  

  
## <a name="see-also"></a>请参阅  
 [选择性 XML 索引 (SXI)](../xml/selective-xml-indexes-sxi.md)   
 [创建、更改和删除选择性 XML 索引](../xml/create-alter-and-drop-selective-xml-indexes.md)  
  
  
