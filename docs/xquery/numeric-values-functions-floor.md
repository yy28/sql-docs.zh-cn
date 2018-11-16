---
title: floor 函数 (XQuery) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: d67244c125b2b85d3db7c0d511a1bf74bcfe91dd
ms.sourcegitcommit: 0f7cf9b7ab23df15624d27c129ab3a539e8b6457
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2018
ms.locfileid: "51293053"
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
  
## <a name="remarks"></a>备注  
 如果类型 *$arg*是三个基本数字类型之一**xs: float**， **xs: double**，或**xs: decimal**，返回类型是与相同 *$arg*类型。 如果类型 *$arg*是从其中一个数值类型派生的类型的返回类型为基的数值类型。  
  
 如果对 fn: floor、 fn: ceiling 或 fn: round 函数的输入**xdt: untypedatomic**，非类型化的数据，它将隐式转换为**xs: double**。 任何其他类型都会生成静态错误。  
  
## <a name="examples"></a>示例  
 本主题提供了一些针对 XML 实例存储在各种中的 XQuery 示例**xml**类型列中的 AdventureWorks 示例数据库。  
  
 可以使用中的工作示例[ceiling 函数 (XQuery)](../xquery/numeric-values-functions-ceiling.md)有关**floor （)** XQuery 函数。 您需要做的就是替换**ceiling （)** 与查询中的函数**floor （)** 函数。  
  
## <a name="implementation-limitations"></a>实现限制  
 限制如下：  
  
-   **Floor （)** 函数将所有整数值都映射到 xs: decimal。  
  
## <a name="see-also"></a>请参阅  
 [ceiling 函数&#40;XQuery&#41;](../xquery/numeric-values-functions-ceiling.md)   
 [round 函数&#40;XQuery&#41;](../xquery/numeric-values-functions-round.md)   
 [针对 xml 数据类型的 XQuery 函数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
