---
title: 数字函数 (XQuery) |Microsoft Docs
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
- number function
- fn:number function
ms.assetid: dff6d19b-765c-4df9-afff-9a0e7be9b91b
author: rothja
ms.author: jroth
ms.openlocfilehash: 31a52f86692d5769fe22f4cf0b5a04ad324c3ac0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930119"
---
# <a name="functions-on-nodes---number"></a>基于节点的函数 - number
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回所指示的节点的数值 *$arg*。  
  
## <a name="syntax"></a>语法  
  
```  
  
fn:number() as xs:double?   
fn:number($arg as node()?) as xs:double?  
```  
  
## <a name="arguments"></a>参数  
 *$arg*  
 将以数字返回其值的节点。  
  
## <a name="remarks"></a>备注  
 如果 *$arg*是未指定，则返回上下文节点，转换为双精度型的数值。 在 SQL Server 中， **fn:number()** 没有仅可以使用上下文相关的谓词的上下文中的参数。 特别要指出的是，它只能在方括号 ([ ]) 内使用。 例如，以下表达式返回 <`ROOT`> 元素。  
  
```  
declare @x xml  
set @x='<ROOT>111</ROOT>'  
select @x.query('/ROOT[number()=111]')  
```  
  
 如果节点的值不是数值简单类型的有效词法表示形式中定义**XML Schema Part 2: datatypes，W3C 建议**，该函数将返回一个空序列。 不支持 NaN。  
  
## <a name="examples"></a>示例  
 本主题提供了一些针对 XML 实例存储在各种 XQuery 示例**xml**类型列中的 AdventureWorks 数据库。  
  
### <a name="a-using-the-number-xquery-function-to-retrieve-the-numeric-value-of-an-attribute"></a>A. 使用 number() XQuery 函数检索属性的数值  
 下面的查询从产品型号 7 的生产进程的第一个生产车间检索 lot size 属性的数值。  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
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
  
-   **Number （)** 函数不是必需的对于查询所示**LotSizeA**属性。 这是一个 XPath 1.0 函数，主要是为了具有向后兼容性才包括在内。  
  
-   有关 XQuery **LotSizeB**指定 number 函数，是冗余的。  
  
-   有关查询**LotSizeD**演示如何使用算术运算中的数字值。  
  
 下面是结果：  
  
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
  
-   **Number （)** 函数只接受节点。 它不接受原子值。  
  
-   不能作为一个数字，返回值时**number （)** 函数返回空序列而不是 NaN。  
  
## <a name="see-also"></a>请参阅  
 [针对 xml 数据类型的 XQuery 函数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
