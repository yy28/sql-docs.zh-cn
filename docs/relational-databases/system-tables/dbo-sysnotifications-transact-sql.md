---
description: dbo.sysnotifications (Transact-SQL)
title: " (Transact-sql) dbo.sys通知 |Microsoft Docs"
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysnotifications_TSQL
- sysnotifications
- sysnotifications_TSQL
- dbo.sysnotifications
dev_langs:
- TSQL
helpviewer_keywords:
- sysnotifications system table
ms.assetid: c5150d18-e8b7-48a7-ada7-77c583af6e41
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8bcfd6b5b52a4f091337d55681be149ccd3f7900
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540346"
---
# <a name="dbosysnotifications-transact-sql"></a>dbo.sysnotifications (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  对每个通知包含一行。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**alert_id**|**int**|警报的 ID。|  
|**operator_id**|**int**|应向其发送此通知的操作员 ID。|  
|**notification_method**|**tinyint**|通知方法：<br /><br /> **1** = 电子邮件<br /><br /> **2** = 寻呼<br /><br /> **4**  = **netsend**<br /><br /> **7** = 全部|  
  
  
