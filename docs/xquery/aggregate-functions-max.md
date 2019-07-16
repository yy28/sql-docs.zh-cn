---
title: max 函数 (XQuery) |Microsoft Docs
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
- max function [XQuery]
- fn:max function
ms.assetid: 5ee625c0-044a-4cda-b210-02b64e619d65
author: rothja
ms.author: jroth
ms.openlocfilehash: e47539a350a2918ef24c47e3c1eca270d4aeb72e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985950"
---
# <a name="aggregate-functions---max"></a>聚合函数 - max
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回一组原子值 *$arg*，其值是否大于所有其他的一个项。  
  
## <a name="syntax"></a>语法  
  
```  
  
fn:max($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>参数  
 *$arg*  
 返回原子值序列中的最大值。  
  
## <a name="remarks"></a>备注  
 所有类型的原子化值传递给**max （)** 必须是同一基类型的子类型。 接受的基类型是支持的类型**gt**操作。 这些类型包括三种内置数值基类型、日期/时间基类型、xs:string、xs:boolean 和 xdt:untypedAtomic。 类型为 xdt:untypedAtomic 的值将转换为 xs:double。 如果混合使用这些类型，或者传递其他类型的其他值，会引发静态错误。  
  
 结果**max （)** 接收传入的类型，如在 xdt: untypedatomic 的情况下 xs: double 的基类型。 如果输入在静态上为空，则暗示为空，并且会引发静态错误。  
  
 **Max （)** 函数返回一个值大于任何其他输入序列中的顺序。 对于 xs:string 值，则使用默认的 Unicode 码位排序规则。 如果无法将 xdt: untypedatomic 值转换为 xs: double，在输入序列中，将忽略值 *$arg*。 如果输入是动态计算的空序列，则返回空序列。  
  
## <a name="examples"></a>示例  
 本主题提供了一些针对 XML 实例存储在各种中的 XQuery 示例**xml**类型列中的[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]数据库。  
  
### <a name="a-using-the-max-xquery-function-to-find-work-center-locations-in-the-manufacturing-process-that-have-the-most-labor-hours"></a>A. 使用 max() XQuery 函数来查找生产过程中工时最多的生产车间。  
 中提供的查询[min 函数 (XQuery)](../xquery/aggregate-functions-min.md)可以重写以使用**max （)** 函数。  
  
## <a name="implementation-limitations"></a>实现限制  
 限制如下：  
  
-   **最大 (** ) 函数将所有整数都映射到 xs: decimal。  
  
-   **Max （)** 不支持对类型 xs: duration 的值的函数。  
  
-   不支持跨基类型边界混合类型的序列。  
  
-   不支持提供排序规则的语法选项。  
  
## <a name="see-also"></a>请参阅  
 [针对 xml 数据类型的 XQuery 函数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
