---
title: "max 函数 (XQuery) |Microsoft 文档"
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
- max function [XQuery]
- fn:max function
ms.assetid: 5ee625c0-044a-4cda-b210-02b64e619d65
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1c3a2ac9b8831fa97843f8de69efca887a2f8437
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="aggregate-functions---max"></a>聚合函数的最大值
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  从一系列原子值，返回*$arg*，其值大于的所有其他的一个项。  
  
## <a name="syntax"></a>语法  
  
```  
  
fn:max($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>参数  
 *$arg*  
 返回原子值序列中的最大值。  
  
## <a name="remarks"></a>注释  
 所有类型的原子化的值传递给**max （)**一定要相同的基类型的子类型。 接受的基类型是支持的类型**gt**操作。 这些类型包括三种内置数值基类型、日期/时间基类型、xs:string、xs:boolean 和 xdt:untypedAtomic。 类型为 xdt:untypedAtomic 的值将转换为 xs:double。 如果没有混合的这些类型，或者如果传递其他类型的其他值时，会引发静态错误。  
  
 结果**max （)**接收传入的类型，如在 xdt:untypedAtomic 的情况下将 xs: double 的基类型。 如果输入在静态上为空，则暗示为空，并且会引发静态错误。  
  
 **Max （)**函数返回一个值大于输入序列中任何其他序列中。 对于 xs:string 值，则使用默认的 Unicode 码位排序规则。 如果 xdt:untypedAtomic 值无法转换为将 xs: double，在输入序列中，将忽略值*$arg*。 如果输入是动态计算的空序列，则返回空序列。  
  
## <a name="examples"></a>示例  
 本主题提供对存储在各种的 XML 实例的 XQuery 示例**xml**类型中的列[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]数据库。  
  
### <a name="a-using-the-max-xquery-function-to-find-work-center-locations-in-the-manufacturing-process-that-have-the-most-labor-hours"></a>A. 使用 max() XQuery 函数来查找生产过程中工时最多的生产车间。  
 中提供的查询[min 函数 (XQuery)](../xquery/aggregate-functions-min.md)可以重新编写为使用**max （)**函数。  
  
## <a name="implementation-limitations"></a>实现限制  
 限制如下：  
  
-   **Max (**) 函数将所有整数都映射到 xs: decimal。  
  
-   **Max （)**不支持对类型 xs: duration 值的函数。  
  
-   不支持跨基类型边界混合类型的序列。  
  
-   不支持提供排序规则的语法选项。  
  
## <a name="see-also"></a>另请参阅  
 [针对 xml 数据类型的 XQuery 函数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  

