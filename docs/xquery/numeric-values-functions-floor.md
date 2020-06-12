---
title: floor 函数（XQuery） |Microsoft Docs
description: 了解 XQuery floor （）函数，该函数返回没有小数部分且不大于其参数值的最大值。
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
- floor function [XQuery]
- fn:floor function
ms.assetid: 4ace57dd-b66e-4b60-a2b9-a1b0f1a0831d
author: rothja
ms.author: jroth
ms.openlocfilehash: 15bdca46fc62832ecd97932b1b71f999f1f80324
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2020
ms.locfileid: "84524388"
---
# <a name="numeric-values-functions---floor"></a>数值函数 - floor
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回每个片段都大于其参数值的最大数。 如果参数是一个空序列，则返回空序列。  
  
## <a name="syntax"></a>语法  
  
```  
  
fn:floor ($arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>参数  
 *$arg*  
 将应用该函数的数字。  
  
## <a name="remarks"></a>注解  
 如果 *$arg*的类型为三个数值基类型之一 **： xs： float**、 **xs： double**或**xs： decimal**，则返回类型与 *$arg*类型相同。 如果 *$arg*的类型是派生自其中一个数值类型的类型，则返回类型为基本数值类型。  
  
 如果向 fn： floor、fn：天花板或 fn： round 函数的输入为**xdt： untypedAtomic**，非类型化数据，则它将隐式转换为**xs： double**。 任何其他类型都会生成静态错误。  
  
## <a name="examples"></a>示例  
 本主题提供了针对在 AdventureWorks 示例数据库的各种**xml**类型列中存储的 xml 实例的 XQuery 示例。  
  
 您可以使用[天花板函数（XQuery）](../xquery/numeric-values-functions-ceiling.md)中的工作示例作为**floor （）** XQuery 函数。 您只需用**floor （）** 函数替换查询中的**天花板（）** 函数。  
  
## <a name="implementation-limitations"></a>实现限制  
 限制如下：  
  
-   **Floor （）** 函数将所有整数值映射到 xs： decimal。  
  
## <a name="see-also"></a>另请参阅  
 [天花板函数 &#40;XQuery&#41;](../xquery/numeric-values-functions-ceiling.md)   
 [&#40;XQuery&#41;循环函数](../xquery/numeric-values-functions-round.md)   
 [针对 xml 数据类型的 XQuery 函数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
