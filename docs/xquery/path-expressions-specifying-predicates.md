---
title: "在路径表达式步骤中指定的谓词 |Microsoft 文档"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- axis step [XQuery]
- predicates [XQuery]
- qualifiers [XQuery]
- path expressions [XQuery]
ms.assetid: 2660ceca-b8b4-4a1f-98a0-719ad5f89f81
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 05290d3f2906136a1d058b63b182877a3226f64e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="path-expressions---specifying-predicates"></a>路径表达式的指定谓词
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  本主题中所述[在 XQuery 中的路径表达式](../xquery/path-expressions-xquery.md)，在路径表达式中的一个轴步骤包括以下组件：  
  
-   [轴](../xquery/path-expressions-specifying-axis.md)。  
  
-   节点测试。 有关详细信息，请参阅[在路径表达式步骤中指定节点测试](../xquery/path-expressions-specifying-node-test.md)。  
  
-   零个或多个谓词。 此为可选项。  
  
 可选的谓词是路径表达式中轴步骤的第三部分。  
  
## <a name="predicates"></a>谓词  
 谓词通过应用指定的测试来筛选节点序列。 谓词表达式用方括号括起来并绑定到路径表达式中的最后一个节点。  
  
 例如，假定的 SQL 参数值 (x) 为**xml**声明数据类型，如在下面的示例所示：  
  
```  
declare @x xml  
set @x = '  
<People>  
  <Person>  
    <Name>John</Name>  
    <Age>24</Age>  
  </Person>  
  <Person>  
    <Name>Goofy</Name>  
    <Age>54</Age>  
  </Person>  
  <Person>  
    <Name>Daffy</Name>  
    <Age>30</Age>  
  </Person>  
</People>  
'  
```  
  
 在这种情况下，下表达式是有效的，它们在三个不同节点级别使用谓词值 [1]。  
  
```  
select @x.query('/People/Person/Name[1]')  
select @x.query('/People/Person[1]/Name')  
select @x.query('/People[1]/Person/Name')  
```  
  
 请注意，在每种情况下，谓词都绑定到应用该谓词的路径表达式中的节点。 例如，第一个路径表达式选择每个 /People/Person 节点中的第一个 <`Name`> 元素，然后使用提供的 XML 实例返回下列内容：  
  
```  
<Name>John</Name><Name>Goofy</Name><Name>Daffy</Name>  
```  
  
 但是，第二个路径表达式选择第一个 /People/Person 节点下的所有 <`Name`> 元素。 因此，它将返回下列内容：  
  
```  
<Name>John</Name>  
```  
  
 括号还可以用来改变谓词的计算顺序。 例如，在下列表达式中，用一组括号来分隔路径 (/People/Person/Name) 和谓词 [1]：  
  
```  
select @x.query('(/People/Person/Name)[1]')  
```  
  
 在此示例中，谓词的应用顺序改变了。 这是因为首先计算括起来的路径 (/People/Person/Name)，然后将谓词 [1] 运算符应用于包含与括起来的路径匹配的所有节点的集合。 如果没有括号，运算顺序就会不同，[1] 将应用为 `child::Name` 节点测试（与第一个路径表达式示例类似）。  
  
### <a name="quantifiers-and-predicates"></a>量词和谓词  
 在谓词自身的括号内可多次使用和添加量词。 例如，接上一个示例，下列是复杂谓词子表达式中多个量词的有效用法。  
  
```  
select @x.query('/People/Person[contains(Name[1], "J") and xs:integer(Age[1]) < 40]/Name/text()')  
```  
  
 谓词表达式的结果将转换为布尔值并作为谓词真值来引用。 结果中仅返回谓词真值为 True 的序列中的节点。 所有其他节点均将放弃。  
  
 例如，下列路径表达式在其第二步中包含一个谓词：  
  
```  
/child::root/child::Location[attribute::LocationID=10]  
```  
  
 此谓词指定的条件应用于所有 <`Location`> 元素节点子级。 结果仅返回 LocationID 属性值为 10 的那些生产车间。  
  
 将在以下 SELECT 语句中执行上一个路径表达式：  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
 /child::AWMI:root/child::AWMI:Location[attribute::LocationID=10]  
')  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
### <a name="computing-predicate-truth-values"></a>计算谓词的真值  
 根据 XQuery 规范，在确定谓词的真值时应用下列规则：  
  
1.  如果谓词表达式的值是一个空序列，则谓词真值为 False。  
  
     例如：  
  
    ```  
    SELECT Instructions.query('  
    declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
     /child::AWMI:root/child::AWMI:Location[attribute::LotSize]  
    ')  
    FROM Production.ProductModel  
    WHERE ProductModelID=7  
    ```  
  
     此查询中的路径表达式仅返回指定了 LotSize 属性的 <`Location`> 元素节点。 如果谓词返回特定 <`Location`> 的空序列，将不在结果中返回该生产车间。  
  
2.  谓词值只能是 xs:integer、 xs: boolean 或节点\*。 节点\*，谓词的计算结果为如果没有任何节点，则为 True 和 False 空序列。 对于任何其他数值类型（如双精度类型和浮点类型），将生成静态类型化错误。 当且仅当所得到的整数等于上下文位置值时，表达式的谓词真值才为 True。 此外，仅整数文本值与**last （)**函数减少到 1 的筛选的步骤表达式的基数。  
  
     例如，下列查询将检索 <`Features`> 元素的第三个子元素节点。  
  
    ```  
    SELECT CatalogDescription.query('  
    declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
    declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
     /child::PD:ProductDescription/child::PD:Features/child::*[3]  
    ')  
    FROM Production.ProductModel  
    WHERE ProductModelID=19  
    ```  
  
     请注意上述查询的以下方面：  
  
    -   表达式中的第三步指定了值为 3 的谓词表达式。 因此，只有对于上下文位置为 3 的节点，此表达式的谓词真值才为 True。  
  
    -   在第三步中还指定了可表示节点测试中的任意节点的通配符 (*)。 但是，谓词将筛选节点，并且仅返回第三个位置的节点。  
  
    -   查询将返回文档根级的 <`ProductDescription`> 元素子级的 <`Features`> 元素子级的第三个子元素节点。  
  
3.  如果谓词表达式的值是一个布尔类型的简单类型值，则谓词真值将等于谓词表达式的值。  
  
     例如，以下查询指定针对**xml**保留 XML 实例时，客户调查 XML 实例的类型变量。 查询检索那些具有子级的客户。 此查询中，在这个位置是\<HasChildren > 1\</HasChildren >。  
  
    ```  
    declare @x xml  
    set @x='  
    <Survey>  
      <Customer CustomerID="1" >  
      <Age>27</Age>  
      <Income>20000</Income>  
      <HasChildren>1</HasChildren>  
      </Customer>  
      <Customer CustomerID="2" >  
      <Age>27</Age>  
      <Income>20000</Income>  
      <HasChildren>0</HasChildren>  
      </Customer>  
    </Survey>  
    '  
    declare @y xml  
    set @y = @x.query('  
      for $c in /child::Survey/child::Customer[( child::HasChildren[1] cast as xs:boolean ? )]  
      return   
          <CustomerWithChildren>  
              { $c/attribute::CustomerID }  
          </CustomerWithChildren>  
    ')  
    select @y  
    ```  
  
     请注意上述查询的以下方面：  
  
    -   中的表达式**为**循环具有两个步骤，且第二个步骤指定的谓词。 此谓词的值是一个布尔类型值。 如果此值为 True，则谓词的真值也为 True。  
  
    -   该查询将返回 <`Customer`> 元素子级，其谓词的值为 True 的\<调查 > 的文档根元素子级。 结果如下：  
  
        ```  
        <CustomerWithChildren CustomerID="1"/>   
        ```  
  
4.  如果谓词表达式的值是一个至少包含一个节点的序列，则谓词真值为 True。  
  
 例如，以下查询检索 ProductModelID 产品型号的 XML 目录说明包括至少一个功能的子元素的 <`Features`> 元素，与关联的命名空间从**wm**前缀。  
  
```  
SELECT ProductModelID  
FROM   Production.ProductModel  
WHERE CatalogDescription.exist('  
             declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
             declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
             /child::PD:ProductDescription/child::PD:Features[wm:*]  
             ') = 1  
```  
  
 请注意上述查询的以下方面：  
  
-   WHERE 子句指定[exist （） 方法 （XML 数据类型）](../t-sql/xml/exist-method-xml-data-type.md)。  
  
-   中的路径表达式**exist （)**方法在第二个步骤中指定的谓词。 如果谓词表达式返回至少一个功能的序列，则该谓词表达式的真值为 True。 在这种情况下，因为**exist （)**方法，则返回 True，则返回 ProductModelID。  
  
## <a name="static-typing-and-predicate-filters"></a>静态类型化和谓词筛选器  
 谓词可能还会影响表达式的静态推断类型。 整数文本值与**last （)**函数减少到最多一个筛选的步骤表达式的基数。  
  
  
