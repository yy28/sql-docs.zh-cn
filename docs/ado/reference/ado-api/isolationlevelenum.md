---
description: IsolationLevelEnum
title: IsolationLevelEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- IsolationLevelEnum
helpviewer_keywords:
- IsolationLevelEnum enumeration [ADO]
ms.assetid: 8e17a7bc-b8a3-4ae2-b6c9-ce088ad31fdf
author: rothja
ms.author: jroth
ms.openlocfilehash: d56051369218f8700ef516526c3f1baf07c7469b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990758"
---
# <a name="isolationlevelenum"></a>IsolationLevelEnum
指定 [连接](./connection-object-ado.md) 对象的事务隔离级别。  
  
|返回的常量|Value|说明|  
|--------------|-----------|-----------------|  
|**adXactUnspecified**|-1|指示提供程序使用的隔离级别与指定的隔离级别不同，但是无法确定该级别。|  
|**adXactChaos**|16|指示无法覆盖来自更高隔离事务的挂起的更改。|  
|**adXactBrowse**|256|指示从一个事务可以查看其他事务中的未提交更改。|  
|**adXactReadUncommitted**|256|与 **adXactBrowse**相同。|  
|**adXactCursorStability**|4096|指示在一个事务中，只可以在提交其他事务后查看这些更改。|  
|**adXactReadCommitted**|4096|与 **adXactCursorStability**相同。|  
|**adXactRepeatableRead**|65536|指示从一个事务中无法看到在其他事务中所做的更改，但该重新查询可以检索新的 **记录集** 对象。|  
|**adXactIsolated**|1048576|指示在隔离其他事务时执行事务。|  
|**adXactSerializable**|1048576|与 **adXactIsolated**相同。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 Package： **.com. 数据**  
  
|返回的常量|  
|--------------|  
|AdoEnums. IsolationLevel。未指定|  
|AdoEnums. IsolationLevel|  
|AdoEnums. IsolationLevel. BROWSE|  
|AdoEnums. IsolationLevel. READUNCOMMITTED|  
|AdoEnums. IsolationLevel. CURSORSTABILITY|  
|AdoEnums. IsolationLevel. READCOMMITTED|  
|AdoEnums. IsolationLevel. REPEATABLEREAD|  
|AdoEnums. IsolationLevel|  
|AdoEnums. IsolationLevel|  
  
## <a name="applies-to"></a>适用于  
 [IsolationLevel 属性](./isolationlevel-property.md)