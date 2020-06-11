---
title: max 函数（XQuery） |Microsoft Docs
description: 了解 XQuery max （）函数，该函数返回一个序列中其值大于所有其他值的项。
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
ms.openlocfilehash: 2b2a7449da7c255d0ddbbed71fef3561f77e294d
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2020
ms.locfileid: "84529981"
---
# <a name="aggregate-functions---max"></a>聚合函数 - max
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  从一个原子值序列（ *$arg*）返回一个值大于所有其他值的项。  
  
## <a name="syntax"></a>语法  
  
```  
  
fn:max($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>参数  
 *$arg*  
 返回原子值序列中的最大值。  
  
## <a name="remarks"></a>注解  
 传递给**max （）** 的原子化值的所有类型都必须是同一基类型的子类型。 接受的基类型是支持**gt**操作的类型。 这些类型包括三种内置数值基类型、日期/时间基类型、xs:string、xs:boolean 和 xdt:untypedAtomic。 类型为 xdt:untypedAtomic 的值将转换为 xs:double。 如果有这些类型的混合，或者如果传递其他类型的其他值，则会引发静态错误。  
  
 **Max （）** 的结果接收传入类型的基类型，例如，在 Xdt： untypedAtomic 的情况下，xs： double。 如果输入在静态上为空，则暗示为空，并且会引发静态错误。  
  
 **Max （）** 函数返回序列中的一个值，该值比输入序列中的任何其他值都大。 对于 xs:string 值，则使用默认的 Unicode 码位排序规则。 如果无法将 xdt： untypedAtomic 值转换为 xs： double，则 *$arg*输入序列中的值将被忽略。 如果输入是动态计算的空序列，则返回空序列。  
  
## <a name="examples"></a>示例  
 本主题提供针对数据库中各种**xml**类型列中存储的 xml 实例的 XQuery 示例 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 。  
  
### <a name="a-using-the-max-xquery-function-to-find-work-center-locations-in-the-manufacturing-process-that-have-the-most-labor-hours"></a>A. 使用 max() XQuery 函数来查找生产过程中工时最多的生产车间。  
 可以重写[min 函数（XQuery）](../xquery/aggregate-functions-min.md)中提供的查询以使用**max （）** 函数。  
  
## <a name="implementation-limitations"></a>实现限制  
 限制如下：  
  
-   **Max （**）函数将所有整数映射到 xs： decimal。  
  
-   不支持**max （）** 函数的类型为 xs： duration 的值。  
  
-   不支持跨基类型边界混合类型的序列。  
  
-   不支持提供排序规则的语法选项。  
  
## <a name="see-also"></a>另请参阅  
 [针对 xml 数据类型的 XQuery 函数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
