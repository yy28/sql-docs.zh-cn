---
title: avg 函数 (XQuery) |Microsoft 文档
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:avg function
- avg function [XQuery]
ms.assetid: 0cc60267-3c56-4a88-8ad7-bb07f0255d56
author: rothja
ms.author: jroth
ms.openlocfilehash: b659aa13a8704a060be12bb015bd0de0fd126562
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985992"
---
# <a name="aggregate-functions---avg"></a>聚合函数 - avg
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回一组数值的平均值。  
  
## <a name="syntax"></a>语法  
  
```  
  
fn:avg($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>参数  
 *$arg*  
 一组要计算平均值的原子值。  
  
## <a name="remarks"></a>备注  
 传递给的原子化值的所有类型**avg （)** 需要的三种内置数值基类型或 xdt: untypedatomic 的一个子类型。 不能使用不同的数值类型。 类型为 xdt:untypedAtomic 的值视为 xs:double。 结果**avg （)** 接收传入的类型，如在 xdt: untypedatomic 的情况下 xs: double 的基类型。  
  
 如果输入在静态上为空，则暗示为空，并且会引发静态错误。  
  
 **Avg （)** 函数返回计算数值的平均值。 例如：  
  
 **sum (** *$arg* **) div 计数 (** *$arg* **)**  
  
 如果 *$arg*是一个空序列，则返回空序列。  
  
 如果无法将 xdt: untypedatomic 值转换为 xs: double，在输入序列中，将忽略该值 *$arg*。  
  
 在所有其他情况下，函数均返回静态错误。  
  
## <a name="examples"></a>示例  
 本主题提供了一些针对 XML 实例存储在各种中的 XQuery 示例**xml**类型列中的 AdventureWorks 数据库。  
  
### <a name="a-using-the-avg-xquery-function-to-find-work-center-locations-in-the-manufacturing-process-in-which-labor-hours-are-greater-than-the-average-for-all-work-center-locations"></a>A. 使用 avg() XQuery 函数来查找生产过程中工时大于所有生产车间的工时平均值的生产车间。  
 您可以重写中提供的查询[min 函数 (XQuery)](../xquery/aggregate-functions-min.md)若要使用**avg （)** 函数。  
  
## <a name="implementation-limitations"></a>实现限制  
 限制如下：  
  
-   **Avg （)** 函数将所有整数都映射到 xs: decimal。  
  
-   **Avg （)** 不支持对类型 xs: duration 的值的函数。  
  
-   不支持跨基类型边界混合类型的序列。  
  
## <a name="see-also"></a>请参阅  
 [针对 xml 数据类型的 XQuery 函数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
