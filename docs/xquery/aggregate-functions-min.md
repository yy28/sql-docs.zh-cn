---
title: "min 函数 (XQuery) |Microsoft 文档"
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- fn:min function
- min function [XQuery]
ms.assetid: db0b7d94-3fa6-488f-96d6-6a9a7d6eda23
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7227bd87057f6cce28d2c63bfe514e3912bf628c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="aggregate-functions---min"></a>聚合函数的最小值
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  从一系列原子值，返回*$arg*，其值是否小于的所有其他的一个项。  
  
## <a name="syntax"></a>语法  
  
```  
  
fn:min($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>参数  
 *$arg*  
 要返回其最小值的一组数值。  
  
## <a name="remarks"></a>注释  
 所有类型的原子化的值传递给**min （)**一定要相同的基类型的子类型。 接受的基类型是支持的类型**gt**操作。 这些类型包括三种内置数值基类型、日期/时间基类型、xs:string、xs:boolean 和 xdt:untypedAtomic。 类型为 xdt:untypedAtomic 的值将转换为 xs:double。 如果没有混合的这些类型，或者如果传递其他类型的其他值时，会引发静态错误。  
  
 结果**min （)**接收传入的类型，如在 xdt:untypedAtomic 的情况下将 xs: double 的基类型。 如果输入是静态 empty，空会进行隐式并返回一个静态的错误。  
  
 **Min （)**函数返回一个值小于输入序列中任何其他序列中。 对于 xs:string 值，则使用默认的 Unicode 码位排序规则。 如果 xdt:untypedAtomic 值无法转换为将 xs: double，在输入序列中，将忽略值*$arg*。 如果输入是动态计算的空序列，则返回空序列。  
  
## <a name="examples"></a>示例  
 本主题提供对存储在各种的 XML 实例的 XQuery 示例**xml** AdventureWorks 数据库中的类型列。  
  
### <a name="a-using-the-min-xquery-function-to-find-the-work-center-location-that-has-the-fewest-labor-hours"></a>A. 使用 min() XQuery 函数查找工时最少的生产车间  
 下面的查询检索产品型号 (ProductModelID=7) 生产过程中工时最少的所有生产车间。 通常返回单个位置，如下所示。 如果多个车间具有相同的最少工时数，则将它们全部返回。  
  
```  
select ProductModelID, Name, Instructions.query('  
  declare namespace AWMI=  
    "http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  for   $Location in /AWMI:root/AWMI:Location  
  where $Location/@LaborHours =  
          min( /AWMI:root/AWMI:Location/@LaborHours )  
return  
  <Location WCID=     "{ $Location/@LocationID }"   
              LaborHrs= "{ $Location/@LaborHours }" />  
  ') as Result   
FROM  Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 请注意上述查询的以下方面：  
  
-   **命名空间**关键字在 XQuery prolog 中的定义的命名空间前缀。 然后，将此前缀用于 XQuery 主体中。  
  
 XQuery 正文构造具有 XML\<位置 > 具有 WCID 元素和**LaborHrs**属性。  
  
-   该查询也检索 ProductModelID 和名称值。  
  
 结果如下：  
  
```  
ProductModelID   Name              Result  
---------------  ----------------  ---------------------------------  
7                HL Touring Frame  <Location WCID="45" LaborHrs="0.5"/>   
```  
  
## <a name="implementation-limitations"></a>实现限制  
 限制如下：  
  
-   **Min （)**函数映射到 xs: decimal 的所有整数。  
  
-   **Min （)**不支持对类型 xs: duration 值的函数。  
  
-   不支持跨基类型边界混合类型的序列。  
  
-   不支持提供排序规则的语法选项。  
  
## <a name="see-also"></a>另请参阅  
 [针对 xml 数据类型的 XQuery 函数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
