---
title: 数据函数 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:data function
- data function [XQuery]
ms.assetid: 511b5d7d-c679-4cb2-a3dd-170cc126f49d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6ac37c6d3a55be4f11a4ad925a950724d5d791d7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62934841"
---
# <a name="data-accessor-functions---data-xquery"></a>数据取值函数 - data (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回指定的每项的类型化的值 *$arg*。  
  
## <a name="syntax"></a>语法  
  
```  
  
fn:data ($arg as item()*) as xdt:untypedAtomic*  
```  
  
## <a name="arguments"></a>参数  
 *$arg*  
 将返回其类型化值的各项的顺序。  
  
## <a name="remarks"></a>备注  
 下列情况适用于类型化值：  
  
-   原子值的类型化值是原子值。  
  
-   文本节点的类型化值是文本节点的字符串值。  
  
-   注释的类型化值是注释的字符串值。  
  
-   处理指令的类型化值是处理指令的内容，不含处理指令目标名称。  
  
-   文档节点的类型化值是文档节点的字符串值。  
  
 下列情况适用于属性节点和元素节点：  
  
-   如果属性节点用 XML 架构类型类型化，则相应地，该节点的类型化值就是类型化值。  
  
-   如果属性节点是非类型化，其类型化的值等于其实例的形式返回的字符串值**xdt: untypedatomic**。  
  
-   如果尚未类型化元素节点，其类型化的值等于其实例的形式返回的字符串值**xdt: untypedatomic**。  
  
 下列情况适用于类型化元素节点：  
  
-   如果元素具有简单内容类型**data （)** 返回元素的类型化的值。  
  
-   如果该节点为复杂类型，包括 xs: anytype， **data （)** 返回静态错误。  
  
 尽管使用**data （)** 函数通常不是强制，如以下示例中，指定中所示**data （)** 函数会显式增加查询的可读性。 有关详细信息，请参阅[XQuery 基础知识](../xquery/xquery-basics.md)。  
  
 不能指定**data （)** 对 XML 构造，如在下面的示例所示：  
  
```  
declare @x xml  
set @x = ''  
select @x.query('data(<SomeNode>value</SomeNode>)')  
```  
  
## <a name="examples"></a>示例  
 本主题提供了一些针对 XML 实例存储在各种 XQuery 示例**xml**类型列中的 AdventureWorks 数据库。  
  
### <a name="a-using-the-data-xquery-function-to-extract-typed-value-of-a-node"></a>A. 使用 data() XQuery 函数提取节点的类型化值  
 以下查询演示了如何**data （)** 函数用于检索属性、 元素和文本节点的值：  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS p1,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
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
  
 下面是结果：  
  
```  
<Root ProductID="19" Feature="parts and labor"/>  
```  
  
 如前文所述， **data （)** 构造属性时，函数是可选。 如果未指定**data （)** 函数，它隐式假设。 下面的查询将与前面的查询生成相同的结果：  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS p1,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
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
  
 以下示例说明了在其中实例**data （)** 函数是必需。  
  
 在下面的查询 **$pd / p1:Specifications / 材料**返回 <`Material`> 元素。 此外，**数据 ($pd/p1:Specifications/材料)** 返回字符数据类型为 xdt: untypedatomic，因为 <`Material`> 是非类型化。 当输入是非类型化、 的结果**data （)** 被类型化为**xdt: untypedatomic**。  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
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
  
 下面是结果：  
  
```  
<Root>  
  <Material>Almuminum Alloy</Material>Almuminum Alloy  
</Root>  
```  
  
 在下面的查询**data($pd/p1:Features/wm:Warranty)** 将返回静态错误，因为 <`Warranty`> 是一个复杂类型元素。  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS p1,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query('  
 <Root>  
   {     /p1:ProductDescription/p1:Features/wm:Warranty }  
   { data(/p1:ProductDescription/p1:Features/wm:Warranty) }  
 </Root>  
 ') as Result  
FROM  Production.ProductModel  
WHERE ProductModelID = 23  
```  
  
## <a name="see-also"></a>请参阅  
 [针对 xml 数据类型的 XQuery 函数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
