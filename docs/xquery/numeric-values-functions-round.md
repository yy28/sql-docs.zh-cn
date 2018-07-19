---
title: round 函数 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- fn:round function
- round function [XQuery]
ms.assetid: 320b572f-bd5b-4055-95a6-dec5718c0041
caps.latest.revision: 29
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 69c9e11d9cb6dda3aa50a2d49e3eb9c55b99a57b
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38055125"
---
# <a name="numeric-values-functions---round"></a>数值函数-round
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回与参数最接近的整数。 如果有多个这样的数，将返回最接近正无穷的那个数。 例如：  
  
 如果参数为 2.5 **round （)** 返回 3。  
  
 如果参数为 2.4999， **round （)** 返回 2。  
  
 如果参数为-2.5， **round （)** 返回-2。  
  
 如果参数为一个空序列， **round （)** 返回空序列。  
  
## <a name="syntax"></a>语法  
  
```  
  
fn:round ( $arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>参数  
 *$arg*  
 将应用该函数的数字。  
  
## <a name="remarks"></a>Remarks  
 如果类型 *$arg*是三个基本数字类型之一**xs: float**， **xs: double**，或**xs: decimal**，返回类型是与相同 *$arg*类型。 如果类型 *$arg*是从其中一个数值类型派生的类型的返回类型为基的数值类型。  
  
 如果输入到**fn: floor**， **fn: ceiling**，或**fn: round** functions 是**xdt: untypedatomic**，非类型化的数据，它将隐式转换为**xs: double**。  
  
 任何其他类型都会生成静态错误。  
  
## <a name="examples"></a>示例  
 本主题提供了一些针对 XML 实例存储在各种 XQuery 示例**xml**类型列中的 AdventureWorks 数据库。  
  
 可以使用中的工作示例[ceiling 函数 (XQuery)](../xquery/numeric-values-functions-ceiling.md)有关**round （)** XQuery 函数。 您需要做的就是替换**ceiling （)** 与查询中的函数**round （)** 函数。  
  
## <a name="implementation-limitations"></a>实现限制  
 限制如下：  
  
-   **Round （)** 函数将整数值映射到 xs: decimal。  
  
-   **Round （)** -0.5e0 和-0e0 之间的 xs: double 和 xs: float 值的函数映射为 0e0，而不是-0e0。  
  
## <a name="see-also"></a>请参阅  
 [floor 函数&#40;XQuery&#41;](../xquery/numeric-values-functions-floor.md)   
 [ceiling 函数&#40;XQuery&#41;](../xquery/numeric-values-functions-ceiling.md)  
  
  
