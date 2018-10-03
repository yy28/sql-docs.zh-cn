---
title: sum 函数 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sum function [XQuery]
- fn:sum function
ms.assetid: 12288f37-b54c-4237-b75e-eedc5fe8f96d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 802c870f2ea22d24d8dfa80144a44f8805a14c96
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47619955"
---
# <a name="aggregate-functions---sum"></a>聚合函数 - sum
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回一列数字的和。  
  
## <a name="syntax"></a>语法  
  
```  
  
fn:sum($arg as xdt:anyAtomicType*) as xdt:anyAtomicType  
```  
  
## <a name="arguments"></a>参数  
 *$arg*  
 要计算和的一列原子值。  
  
## <a name="remarks"></a>备注  
 所有类型的原子化值传递给**sum （)** 必须是同一基类型的子类型。 接受的基类型为三种内置数字基类型或 xdt:untypedAtomic。 类型为 xdt:untypedAtomic 的值将转换为 xs:double。 如果混合使用这些类型，或者传递其他类型的其他值，会引发静态错误。  
  
 结果**sum （)** 接收传入的类型，如 xdt: untypedatomic，对于 xs: double 的基类型，即使输入或者是空序列。 如果输入在静态下为空，则对于 xs:integer 的静态和动态类型，结果都为 0。  
  
 **Sum （)** 函数将返回数字值的总和。 如果无法将 xdt: untypedatomic 值转换为 xs: double，在输入序列中，将忽略值 *$arg*。 如果输入是动态计算的空序列，则返回的所用基类型的值为 0。  
  
 当发生溢出或超出范围异常时，函数将返回一个运行时错误。  
  
## <a name="examples"></a>示例  
 本主题提供了一些针对 XML 实例存储在各种中的 XQuery 示例**xml**类型列中的[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]数据库。  
  
### <a name="a-using-the-sum-xquery-function-to-find-the-total-combined-number-of-labor-hours-for-all-work-center-locations-in-the-manufacturing-process"></a>A. 使用 sum() XQuery 函数查找计算生产过程中所有生产车间的总工时  
 下面的查询查找在生产（已存储其生产说明的）所有产品型号的过程中所有生产车间的总工时。  
  
```  
SELECT Instructions.query('         
   declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";         
  <ProductModel PMID= "{ sql:column("Production.ProductModel.ProductModelID") }"         
  ProductModelName = "{ sql:column("Production.ProductModel.Name") }" >         
   <TotalLaborHrs>         
     { sum(//AWMI:Location/@LaborHours) }         
   </TotalLaborHrs>         
 </ProductModel>         
    ') as Result         
FROM Production.ProductModel         
WHERE Instructions is not NULL         
```  
  
 下面是部分结果：  
  
```  
<ProductModel PMID="7" ProductModelName="HL Touring Frame">  
   <TotalLaborHrs>12.75</TotalLaborHrs>  
</ProductModel>  
<ProductModel PMID="10" ProductModelName="LL Touring Frame">  
  <TotalLaborHrs>13</TotalLaborHrs>  
</ProductModel>  
...  
```  
  
 您可以编写查询以生成关系结果，而不以 XML 形式返回结果，如下面的查询所示：  
  
```  
SELECT ProductModelID,         
        Name,         
        Instructions.value('declare namespace   
      AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";         
    sum(//AWMI:Location/@LaborHours)', 'float') as TotalLaborHours         
FROM Production.ProductModel         
WHERE Instructions is not NULL          
```  
  
 这是部分结果：  
  
```  
ProductModelID Name                 TotalLaborHours         
-------------- -------------------------------------------------  
7              HL Touring Frame           12.75                   
10             LL Touring Frame           13                      
43             Touring Rear Wheel         3                       
...  
```  
  
### <a name="implementation-limitations"></a>实现限制  
 限制如下：  
  
-   仅单参数版本的**sum （)** 支持。  
  
-   如果输入是动态计算的空序列，则返回的所用基类型（而不是 xs:integer 类型）的值为 0。  
  
-   **Sum （)** 函数将所有整数都映射到 xs: decimal。  
  
-   **Sum （)** 不支持对类型 xs: duration 的值的函数。  
  
-   不支持跨基类型边界混合类型的序列。  
  
-   sum((xs:double(“INF”), xs:double(“-INF”))) 将引发域错误。  
  
## <a name="see-also"></a>请参阅  
 [针对 xml 数据类型的 XQuery 函数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
