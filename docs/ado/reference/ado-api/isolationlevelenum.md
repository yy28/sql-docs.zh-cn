---
title: IsolationLevelEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 366892f51207e7d89f643510f9becb664bb098c6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47684195"
---
# <a name="isolationlevelenum"></a>IsolationLevelEnum
指定的事务隔离级别[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adXactUnspecified**|-1|指示提供程序正在使用不同的隔离级别与指定，但不能确定级别。|  
|**adXactChaos**|16|指示，挂起的更改程度更高隔离级别事务中不能被覆盖。|  
|**adXactBrowse**|256|指示从一个事务，可以查看未提交的更改在其他事务中。|  
|**adXactReadUncommitted**|256|与相同**adXactBrowse**。|  
|**adXactCursorStability**|4096|指示从一个事务，可以查看更改在其他事务中仅已提交之后。|  
|**adXactReadCommitted**|4096|与相同**adXactCursorStability**。|  
|**adXactRepeatableRead**|65536|指示不能从一个事务看到在其他事务中所做的更改，但该再次查询可以检索新**记录集**对象。|  
|**adXactIsolated**|1048576|指示事务进行的其他事务隔离。|  
|**adXactSerializable**|1048576|与相同**adXactIsolated**。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 等效项  
 包： **com.ms.wfc.data**  
  
|常量|  
|--------------|  
|AdoEnums.IsolationLevel.UNSPECIFIED|  
|AdoEnums.IsolationLevel.CHAOS|  
|AdoEnums.IsolationLevel.BROWSE|  
|AdoEnums.IsolationLevel.READUNCOMMITTED|  
|AdoEnums.IsolationLevel.CURSORSTABILITY|  
|AdoEnums.IsolationLevel.READCOMMITTED|  
|AdoEnums.IsolationLevel.REPEATABLEREAD|  
|AdoEnums.IsolationLevel.ISOLATED|  
|AdoEnums.IsolationLevel.SERIALIZABLE|  
  
## <a name="applies-to"></a>适用范围  
 [IsolationLevel 属性](../../../ado/reference/ado-api/isolationlevel-property.md)
