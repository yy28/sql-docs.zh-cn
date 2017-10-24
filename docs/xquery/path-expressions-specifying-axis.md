---
title: "在路径表达式步骤中指定轴 |Microsoft 文档"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- attribute axis [SQL Server]
- axis step [XQuery]
- descendant axis
- self axis
- path expressions [XQuery]
- child axis
- descendant-or-self axis
- parent axis
ms.assetid: c44fb843-0626-4496-bde0-52ca0bac0a9e
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c34c230f6df65610466e087da5707622c3911e42
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="path-expressions---specifying-axis"></a>路径表达式的指定轴
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  路径表达式中的轴步骤包括以下部分：  
  
-   轴  
  
-   A[节点测试](../xquery/path-expressions-specifying-node-test.md)  
  
-   [（可选） 的零个或多个步骤限定符](../xquery/path-expressions-specifying-predicates.md)  
  
 有关详细信息，请参阅[路径表达式 &#40;XQuery &#41;](../xquery/path-expressions-xquery.md).  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的 XQuery 实现支持以下轴步骤：  
  
|Axis|Description|  
|----------|-----------------|  
|**子**|返回上下文节点的子级。|  
|**后代**|返回上下文节点的所有后代。|  
|**父**|返回上下文节点的父级。|  
|**属性**|返回上下文节点的属性。|  
|**自助**|返回上下文节点本身。|  
|**后代或自助**|返回上下文节点及其所有后代。|  
  
 所有这些轴，除**父**轴，是正轴。 **父**轴是反向轴，因为它会在文档层次结构中向后搜索。 例如，相对路径表达式 `child::ProductDescription/child::Summary` 包含两个步骤，每个步骤均指定一个 `child` 轴。 第一步检索\<ProductDescription > 元素的上下文节点的子级。 每个\<ProductDescription > 元素节点的第二步检索\<摘要 > 子元素节点。  
  
 相对路径表达式 `child::root/child::Location/attribute::LocationID` 包含三个步骤。 前两个步骤各指定一个 `child` 轴，第三步是指定 `attribute` 轴。 对生产说明 XML 文档中的执行时**Production.ProductModel**表，该表达式将返回`LocationID`属性\<位置 >的子元素节点\<根 > 元素。  
  
## <a name="examples"></a>示例  
 针对指定的此主题中的查询示例**xml**类型中的列**AdventureWorks**数据库。  
  
### <a name="a-specifying-a-child-axis"></a>A. 指定 child 轴  
 对于特定产品的模型中，以下查询会检索\<功能 > 元素节点子级的\<ProductDescription > 元素节点从存储中的产品目录说明`Production.ProductModel`表。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  /child::PD:ProductDescription/child::PD:Features')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 请注意上述查询的以下方面：  
  
-   `query()`方法**xml**数据类型指定的路径表达式。  
  
-   路径表达式中的两个步骤都指定一个 `child` 轴和节点名称（`ProductDescription` 和 `Features`）作为节点测试。 有关节点测试的信息，请参阅[在路径表达式步骤中指定节点测试](../xquery/path-expressions-specifying-node-test.md)。  
  
### <a name="b-specifying-descendant-and-descendant-or-self-axes"></a>B. 指定 descendant 轴和 descendant-or-self 轴  
 以下示例使用 descendant 轴和 descendant-or-self 轴。 此示例中的查询指定针对**xml**类型变量。 该 XML 实例经过简化以方便说明生成的结果中的差异。  
  
```  
declare @x xml  
set @x='  
<a>  
 <b>text1  
   <c>text2  
     <d>text3</d>  
   </c>  
 </b>  
</a>'  
declare @y xml  
set @y = @x.query('  
  /child::a/child::b  
')  
select @y  
```  
  
 在以下结果中，表达式返回 `<b>` 元素节点的 `<a>` 元素节点子级：  
  
```  
<b>text1  
   <c>text2  
     <d>text3</d>  
   </c>  
</b>  
```  
  
 在此表达式中，如果为路径表达式指定了 descendant 轴   
  
 `/child::a/child::b/descendant::*`，则您请求的是 <`b`> 元素节点的所有后代。  
  
 节点测试中的星号 (*) 以一个节点测试表示节点名称。 因此，descendant 轴的主节点类型（元素节点）确定返回节点的类型。 即表达式返回所有元素节点。 但不返回文本节点。 有关主节点类型和节点测试其关系的详细信息，请参阅[在路径表达式步骤中指定节点测试](../xquery/path-expressions-specifying-node-test.md)主题。  
  
 此时返回元素节点 <`c`> 和 <`d`>，结果如下所示：  
  
```  
<c>text2  
     <d>text3</d>  
</c>  
<d>text3</d>  
```  
  
 如果您指定的是 descendant-or-self 轴而不是 descendant 轴，`/child::a/child::b/descendant-or-self::*` 返回上下文节点、元素 <`b`> 及其后代。  
  
 结果如下：  
  
```  
<b>text1  
   <c>text2  
     <d>text3</d>  
   </c>  
</b>  
  
<c>text2  
     <d>text3</d>  
</c>  
  
<d>text3</d>   
```  
  
 下面的示例查询针对**AdventureWorks**数据库检索的所有子代元素节点 <`Features`> 子元素的 <`ProductDescription`> 元素：  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  /child::PD:ProductDescription/child::PD:Features/descendant::*  
')  
FROM  Production.ProductModel  
WHERE ProductModelID=19  
```  
  
### <a name="c-specifying-a-parent-axis"></a>C. 指定 parent 轴  
 以下查询从 `Production.ProductModel` 表中存储的产品目录 XML 文档返回 <`ProductDescription`> 元素的 <`Summary`> 元素子级。  
  
 此示例使用 parent 轴来返回 <`Feature`> 元素的父级，并检索 <`ProductDescription`> 元素的 <`Summary`> 元素子级。  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  
/child::PD:ProductDescription/child::PD:Features/parent::PD:ProductDescription/child::PD:Summary  
')  
FROM   Production.ProductModel  
WHERE  ProductModelID=19  
  
```  
  
 在此查询示例中，路径表达式使用 `parent` 轴。 您可以重写该表达式，不使用 parent 轴，如下所示：  
  
```  
/child::PD:ProductDescription[child::PD:Features]/child::PD:Summary  
```  
  
 以下是一个关于 parent 轴的更为有用的示例。  
  
 存储在每个产品型号目录说明**CatalogDescription**列**ProductModel**表具有`<ProductDescription>`元素具有`ProductModelID`属性和`<Features>`子元素，如以下片段中所示：  
  
```  
<ProductDescription ProductModelID="..." >  
  ...  
  <Features>  
    <Feature1>...</Feature1>  
    <Feature2>...</Feature2>  
   ...  
</ProductDescription>  
```  
  
 查询在 FLWOR 语句中设置了一个迭代器变量 `$f`，以返回 `<Features>` 元素的元素子级。 有关详细信息，请参阅[FLWOR 语句和迭代 &#40;XQuery &#41;](../xquery/flwor-statement-and-iteration-xquery.md). 对于每个功能，`return` 子句都构造一个以下形式的 XML：  
  
```  
<Feature ProductModelID="...">...</Feature>  
<Feature ProductModelID="...">...</Feature>  
```  
  
 为了给每个 `ProductModelID`> 元素添加 `<Feature`，指定了 `parent` 轴：  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
  for $f in /child::PD:ProductDescription/child::PD:Features/child::*  
  return  
   <Feature  
     ProductModelID="{ ($f/parent::PD:Features/parent::PD:ProductDescription/attribute::ProductModelID)[1]}" >  
          { $f }  
   </Feature>  
')  
FROM  Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 下面是部分结果：  
  
```  
<Feature ProductModelID="19">  
  <wm:Warranty   
   xmlns:wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
    <wm:Description>parts and labor</wm:Description>  
  </wm:Warranty>  
</Feature>  
<Feature ProductModelID="19">  
  <wm:Maintenance   
   xmlns:wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <wm:NoOfYears>10 years</wm:NoOfYears>  
    <wm:Description>maintenance contract available through your dealer   
                  or any AdventureWorks retail store.</wm:Description>  
  </wm:Maintenance>  
</Feature>  
<Feature ProductModelID="19">  
  <p1:wheel   
   xmlns:p1="http://www.adventure-works.com/schemas/OtherFeatures">  
      High performance wheels.  
  </p1:wheel>  
</Feature>  
```  
  
 请注意，在路径表达式中添加了谓词 `[1]`，这是为了确保返回单一值。  
  
  

