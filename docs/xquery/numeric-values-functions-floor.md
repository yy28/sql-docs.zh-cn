---
title: floor 函数 (XQuery) |Microsoft 文档
ms.custom: ''
ms.date: 03/09/2017
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
- floor function [XQuery]
- fn:floor function
ms.assetid: 4ace57dd-b66e-4b60-a2b9-a1b0f1a0831d
caps.latest.revision: 27
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 718d95f84d7fde816b243de61ea21122e21294c1
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="numeric-values-functions---floor"></a>数字值函数-floor
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回每个片段都大于其参数值的最大数。 如果参数是一个空序列，则返回空序列。  
  
## <a name="syntax"></a>语法  
  
```  
  
fn:floor ($arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>参数  
 *$arg*  
 将应用该函数的数字。  
  
## <a name="remarks"></a>注释  
 如果的一种 *$arg*是三个数值基类型，之一**xs:float**，**将 xs: double**，或**xs: decimal**，返回类型是相同 *$arg*类型。 如果的一种 *$arg*是派生自的数值类型之一的类型的返回类型为基的数值类型。  
  
 如果输入为 fn:floor、 fn:ceiling 或 fn:round 函数**xdt:untypedAtomic**，非类型化的数据，它被隐式强制转换为**将 xs: double**。 任何其他类型都会生成静态错误。  
  
## <a name="examples"></a>示例  
 本主题提供对存储在各种的 XML 实例的 XQuery 示例**xml**类型列中的 AdventureWorks 示例数据库。  
  
 你可以使用中的工作示例[ceiling 函数 (XQuery)](../xquery/numeric-values-functions-ceiling.md)为**floor （)** XQuery 函数。 你所要做的就是替换**ceiling()** 在查询中使用的函数**floor （)** 函数。  
  
## <a name="implementation-limitations"></a>实现限制  
 限制如下：  
  
-   **Floor （)** 函数将所有的整数值映射到 xs: decimal。  
  
## <a name="see-also"></a>另请参阅  
 [ceiling 函数&#40;XQuery&#41;](../xquery/numeric-values-functions-ceiling.md)   
 [round 函数&#40;XQuery&#41;](../xquery/numeric-values-functions-round.md)   
 [针对 xml 数据类型的 XQuery 函数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
