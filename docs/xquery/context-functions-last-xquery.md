---
title: last 函数 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
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
- last function [XQuery]
- fn:last function
ms.assetid: dc92086e-3b01-4b0b-9f54-3bbf306cf7ae
caps.latest.revision: 25
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 33b7afe5bdef612fe48938d8118c17d5d6e7a512
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38038435"
---
# <a name="context-functions---last-xquery"></a>上下文函数-last (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回当前处理的序列中的项数。 具体来说，它返回序列中最后一项的整数索引。 序列中第一项的索引值为 1。  
  
## <a name="syntax"></a>语法  
  
```  
  
fn:last() as xs:integer  
```  
  
## <a name="remarks"></a>Remarks  
 在 SQL Server 中， **fn:last()** 仅可以使用上下文相关的谓词的上下文中。 特别要指出的是，它只能在方括号 (`[ ]`) 内使用。  
  
## <a name="examples"></a>示例  
 本主题提供了一些针对 XML 实例存储在各种中的 XQuery 示例**xml**类型列中的 AdventureWorks 数据库。  
  
### <a name="a-using-the-last-xquery-function-to-retrieve-the-last-two-manufacturing-steps"></a>A. 使用 last() XQuery 函数检索最后两个生产步骤  
 下面的查询检索某个特定生产模型的最后两个生产步骤。 值，返回生产步骤数**last （)** 函数使用此查询中检索最后两个生产步骤。  
  
```  
SELECT ProductModelID, Instructions.query('   
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  <LastTwoManuSteps>  
   <Last-1Step>   
     { (/AWMI:root/AWMI:Location)[1]/AWMI:step[(last()-1)]/text() }  
   </Last-1Step>  
   <LastStep>   
     { (/AWMI:root/AWMI:Location)[1]/AWMI:step[last()]/text() }  
   </LastStep>  
  </LastTwoManuSteps>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 在前面的查询中， **last （)** 函数，在 /`/AWMI:root//AWMI:Location)[1]/AWMI:step[last()]`返回生产步骤数。 此值用于检索生产车间的最后一个生产步骤。  
  
 结果如下：  
  
```  
ProductModelID Result    
-------------- -------------------------------------  
7      <LastTwoManuSteps>  
         <Last-1Step>  
            When finished, inspect the forms for defects per   
            Inspection Specification .  
         </Last-1Step>  
         <LastStep>Remove the frames from the tool and place them   
            in the Completed or Rejected bin as appropriate.  
         </LastStep>  
       </LastTwoManuSteps>  
```  
  
## <a name="see-also"></a>请参阅  
 [针对 xml 数据类型的 XQuery 函数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
