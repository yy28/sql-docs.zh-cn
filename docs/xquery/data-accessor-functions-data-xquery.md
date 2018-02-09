---
title: "数据函数 (XQuery) |Microsoft 文档"
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- fn:data function
- data function [XQuery]
ms.assetid: 511b5d7d-c679-4cb2-a3dd-170cc126f49d
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bc544e5f0c1f735f0a4b174a67416e52efae1da1
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="data-accessor-functions---data-xquery"></a>数据访问器函数的数据 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回由指定每个项的类型化的值*$arg*。  
  
## <a name="syntax"></a>语法  
  
```  
  
fn:data ($arg as item()*) as xdt:untypedAtomic*  
```  
  
## <a name="arguments"></a>参数  
 *$arg*  
 将返回其类型化值的各项的顺序。  
  
## <a name="remarks"></a>注释  
 下列情况适用于类型化值：  
  
-   原子值的类型化值是原子值。  
  
-   文本节点的类型化值是文本节点的字符串值。  
  
-   注释的类型化值是注释的字符串值。  
  
-   处理指令的类型化值是处理指令的内容，不含处理指令目标名称。  
  
-   文档节点的类型化值是文档节点的字符串值。  
  
 下列情况适用于属性节点和元素节点：  
  
-   如果属性节点用 XML 架构类型类型化，则相应地，该节点的类型化值就是类型化值。  
  
-   如果非类型化的属性节点，其类型化的值等于其实例的形式返回的字符串值**xdt:untypedAtomic**。  
  
-   如果元素节点未类型化，其类型化的值等于其实例的形式返回的字符串值**xdt:untypedAtomic**。  
  
 下列情况适用于类型化元素节点：  
  
-   如果元素具有简单内容类型， **data （)**返回元素的类型化的值。  
  
-   如果节点为复杂类型，包括 xs: anytype， **data （)**返回静态错误。  
  
 尽管使用**data （)**函数是经常是可选的如以下示例中，指定所示**data （)**函数显式提高了查询可读性。 有关详细信息，请参阅[XQuery 基础知识](../xquery/xquery-basics.md)。  
  
 不能指定**data （)**上构造 XML，如在下面的示例所示：  
  
```  
declare @x xml  
set @x = ''  
select @x.query('data(<SomeNode>value</SomeNode>)')  
```  
  
## <a name="examples"></a>示例  
 本主题提供对 XML 实例存储在各种 XQuery 示例**xml** AdventureWorks 数据库中的类型列。  
  
### <a name="a-using-the-data-xquery-function-to-extract-typed-value-of-a-node"></a>A. 使用 data() XQuery 函数提取节点的类型化值  
 以下查询说明了如何**data （)**函数用于检索属性、 元素和文本节点的值：  
  
```  
WITH XMLNAMESPACES (  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS p1,  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query(N'  
 for $pd in //p1:ProductDescription  
 return   
    <Root   
      ProductID = "{ data( ($pd//@ProductModelID)[1] ) }"   
      Feature =   "{ data( ($pd/p1:Features/wm:Warranty/wm:Description)[1] ) }" >  
    </Root>  
 ') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 结果如下：  
  
```  
<Root ProductID="19" Feature="parts and labor"/>  
```  
  
 如前文所述， **data （)**函数是可选的当你在构造属性。 如果不指定**data （)**函数，隐式假设。 下面的查询将与前面的查询生成相同的结果：  
  
```  
WITH XMLNAMESPACES (  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS p1,  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query('  
      for $pd in //p1:ProductDescription  
         return   
          <Root    
                ProductID = "{ ($pd/@ProductModelID)[1] }"    
                Feature =   "{ ($pd/p1:Features/wm:Warranty/wm:Description)[1] }" >  
           </Root>  
 ') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 以下示例说明了在其中实例**data （)**函数是必需。  
  
 在下面的查询， **$pd / p1:Specifications / 材料**返回 <`Material`> 元素。 此外，**数据 ($pd/p1:Specifications/材料)**返回字符数据类型化为 xdt:untypedAtomic，因为 <`Material`> 是非类型化。 当输入是非类型化、 的结果**data （)**被类型化为**xdt:untypedAtomic**。  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      for $pd in //p1:ProductDescription  
         return   
          <Root>  
             { $pd/p1:Specifications/Material }  
             { data($pd/p1:Specifications/Material) }  
           </Root>  
 ') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 结果如下：  
  
```  
<Root>  
  <Material>Almuminum Alloy</Material>Almuminum Alloy  
</Root>  
```  
  
 在下面的查询， **data($pd/p1:Features/wm:Warranty)**返回静态的错误，因为 <`Warranty`> 是一个复杂类型元素。  
  
```  
WITH XMLNAMESPACES (  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS p1,  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query('  
 <Root>  
   {     /p1:ProductDescription/p1:Features/wm:Warranty }  
   { data(/p1:ProductDescription/p1:Features/wm:Warranty) }  
 </Root>  
 ') as Result  
FROM  Production.ProductModel  
WHERE ProductModelID = 23  
```  
  
## <a name="see-also"></a>另请参阅  
 [针对 xml 数据类型的 XQuery 函数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
