---
title: round 函数 (XQuery) |Microsoft 文档
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.service: ''
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
ms.workload: Inactive
ms.openlocfilehash: cd4fa2060667fc914e8ef52f998f162bb8b27976
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="numeric-values-functions---round"></a>舍入数字值功能-
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回与参数最接近的整数。 如果有多个这样的数，将返回最接近正无穷的那个数。 例如：  
  
 如果参数为 2.5， **round （)** 返回 3。  
  
 如果参数是 2.4999， **round （)** 返回 2。  
  
 如果参数是-2.5， **round （)** 返回-2。  
  
 如果参数为空序列， **round （)** 返回空序列。  
  
## <a name="syntax"></a>语法  
  
```  
  
fn:round ( $arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>参数  
 *$arg*  
 将应用该函数的数字。  
  
## <a name="remarks"></a>注释  
 如果的一种 *$arg*是三个数值基类型，之一**xs:float**，**将 xs: double**，或**xs: decimal**，返回类型是相同 *$arg*类型。 如果的一种 *$arg*是派生自的数值类型之一的类型的返回类型为基的数值类型。  
  
 如果输入到**fn:floor**， **fn:ceiling**，或**fn:round**函数是**xdt:untypedAtomic**，非类型化的数据，它被隐式强制转换为**将 xs: double**。  
  
 任何其他类型都会生成静态错误。  
  
## <a name="examples"></a>示例  
 本主题提供对 XML 实例存储在各种 XQuery 示例**xml** AdventureWorks 数据库中的类型列。  
  
 你可以使用中的工作示例[ceiling 函数 (XQuery)](../xquery/numeric-values-functions-ceiling.md)为**round （)** XQuery 函数。 你所要做的就是替换**ceiling()** 在查询中使用的函数**round （)** 函数。  
  
## <a name="implementation-limitations"></a>实现限制  
 限制如下：  
  
-   **Round （)** 函数映射到 xs: decimal 整数值。  
  
-   **Round （)** -0.5e0 和 0e0 之间的将 xs: double 和 xs:float 值的函数映射到而不是-0e0 0e0。  
  
## <a name="see-also"></a>另请参阅  
 [floor 函数&#40;XQuery&#41;](../xquery/numeric-values-functions-floor.md)   
 [ceiling 函数&#40;XQuery&#41;](../xquery/numeric-values-functions-ceiling.md)  
  
  
