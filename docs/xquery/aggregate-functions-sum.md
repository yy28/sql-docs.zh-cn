---
title: "sum 函数 (XQuery) |Microsoft 文档"
ms.custom: 
ms.date: 03/09/2017
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
- sum function [XQuery]
- fn:sum function
ms.assetid: 12288f37-b54c-4237-b75e-eedc5fe8f96d
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3ae0eacebba36dd75537a36cfaf0ce46ba43f332
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="aggregate-functions---sum"></a>聚合函数-求和
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回一列数字的和。  
  
## <a name="syntax"></a>语法  
  
```  
  
fn:sum($arg as xdt:anyAtomicType*) as xdt:anyAtomicType  
```  
  
## <a name="arguments"></a>参数  
 *$arg*  
 要计算和的一列原子值。  
  
## <a name="remarks"></a>注释  
 所有类型的原子化的值传递给**sum （)**一定要相同的基类型的子类型。 接受的基类型为三种内置数字基类型或 xdt:untypedAtomic。 类型为 xdt:untypedAtomic 的值将转换为 xs:double。 如果没有混合的这些类型，或者如果传递其他类型的其他值时，会引发静态错误。  
  
 结果**sum （)**接收传入的类型，如 xdt:untypedAtomic，对于将 xs: double 的基类型，即使输入 （可选） 是空的序列。 如果输入在静态下为空，则对于 xs:integer 的静态和动态类型，结果都为 0。  
  
 **Sum （)**函数将返回数字值的总和。 如果 xdt:untypedAtomic 值无法转换为将 xs: double，在输入序列中，将忽略值*$arg*。 如果输入是动态计算的空序列，则返回的所用基类型的值为 0。  
  
 当发生溢出或超出范围异常时，函数将返回一个运行时错误。  
  
## <a name="examples"></a>示例  
 本主题提供对存储在各种的 XML 实例的 XQuery 示例**xml**类型中的列[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]数据库。  
  
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
  
 下面是部分结果：  
  
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
  
-   只有单个自变量版本的**sum （)**支持。  
  
-   如果输入是动态计算的空序列，则返回的所用基类型（而不是 xs:integer 类型）的值为 0。  
  
-   **Sum （)**函数映射到 xs: decimal 的所有整数。  
  
-   **Sum （)**不支持对类型 xs: duration 值的函数。  
  
-   不支持跨基类型边界混合类型的序列。  
  
-   sum((xs:double(“INF”), xs:double(“-INF”))) 将引发域错误。  
  
## <a name="see-also"></a>另请参阅  
 [针对 xml 数据类型的 XQuery 函数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  

