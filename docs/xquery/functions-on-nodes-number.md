---
title: "数字函数 (XQuery) |Microsoft 文档"
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
- number function
- fn:number function
ms.assetid: dff6d19b-765c-4df9-afff-9a0e7be9b91b
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 85882cd83303223917300175059f0905a2d6ad2d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="functions-on-nodes---number"></a>节点的数量上的函数
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回指示的节点的数值*$arg*。  
  
## <a name="syntax"></a>语法  
  
```  
  
fn:number() as xs:double?   
fn:number($arg as node()?) as xs:double?  
```  
  
## <a name="arguments"></a>参数  
 *$arg*  
 将以数字返回其值的节点。  
  
## <a name="remarks"></a>注释  
 如果*$arg*是未指定，则返回的上下文节点，转换为双精度，数字值。 在 SQL Server， **fn:number()**没有仅可以依赖于上下文的谓词的上下文中使用的参数。 特别要指出的是，它只能在方括号 ([ ]) 内使用。 例如，下面的表达式返回 <`ROOT`> 元素。  
  
```  
declare @x xml  
set @x='<ROOT>111</ROOT>'  
select @x.query('/ROOT[number()=111]')  
```  
  
 如果节点的值不是有效的词法表示形式的数值的简单类型中定义**XML Schema Part 2:Datatypes，W3C 建议**，该函数将返回空序列。 不支持 NaN。  
  
## <a name="examples"></a>示例  
 本主题提供对 XML 实例存储在各种 XQuery 示例**xml** AdventureWorks 数据库中的类型列。  
  
### <a name="a-using-the-number-xquery-function-to-retrieve-the-numeric-value-of-an-attribute"></a>A. 使用 number() XQuery 函数检索属性的数值  
 下面的查询从产品型号 7 的生产进程的第一个生产车间检索 lot size 属性的数值。  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     for $i in (//AWMI:root//AWMI:Location)[1]  
     return   
       <Location LocationID="{ ($i/@LocationID) }"   
                   LotSizeA="{  $i/@LotSize }"  
                   LotSizeB="{  number($i/@LotSize) }"  
                   LotSizeC="{ number($i/@LotSize) + 1 }" >  
  
       </Location>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 请注意上述查询的以下方面：  
  
-   **Number （） 来**函数不是必需的如所示的查询**LotSizeA**属性。 这是一个 XPath 1.0 函数，主要是为了具有向后兼容性才包括在内。  
  
-   为 XQuery **LotSizeB**指定数值的函数，为冗余。  
  
-   有关查询**LotSizeD**演示如何使用算术运算的数值。  
  
 结果如下：  
  
```  
ProductModelID   Result  
----------------------------------------------  
7              <Location LocationID="10"   
                         LotSizeA="100"   
                         LotSizeB="100"   
                         LotSizeC="101" />  
```  
  
### <a name="implementation-limitations"></a>实现限制  
 限制如下：  
  
-   **Number （） 来**函数只接受节点。 它不接受原子值。  
  
-   不能为数字，返回值时**number （） 来**函数将返回而不是 NaN 的空序列。  
  
## <a name="see-also"></a>另请参阅  
 [针对 xml 数据类型的 XQuery 函数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
