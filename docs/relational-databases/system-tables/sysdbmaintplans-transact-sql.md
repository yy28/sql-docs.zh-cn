---
title: sysdbmaintplans (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdbmaintplans_TSQL
- sysdbmaintplans
dev_langs:
- TSQL
helpviewer_keywords:
- sysdbmaintplans system table
ms.assetid: 0363296a-3082-48a9-9eb5-a1020b2f541a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0525a50b30036470336dafe10c78a42218486c63
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47774665"
---
# <a name="sysdbmaintplans-transact-sql"></a>sysdbmaintplans (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  此表包含在[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]若要保留的现有信息从以前版本的实例升级[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不更改此表的内容。 此表存储中**msdb**数据库。  
  
 [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  

  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**plan_id**|**uniqueidentifier**|数据库维护计划 ID。|  
|**plan_name**|**sysname**|数据库维护计划名称。|  
|**date_created**|**datetime**|创建数据库维护计划的日期。|  
|**所有者**|**sysname**|数据库维护计划的所有者。|  
|**max_history_rows**|**int**|在系统表中，为记录数据库维护计划的历史所分配的最大行数。|  
|**remote_history_server**|**sysname**|远程服务器的名称，可以将历史报表写入该远程服务器中。|  
|**max_remote_history_rows**|**int**|远程服务器上的系统表中所分配的最大行数，可以将历史报表写入该远程服务器中。|  
|**user_defined_1**|**int**|默认值为 NULL。|  
|**user_defined_2**|**nvarchar(100)**|默认值为 NULL。|  
|**user_defined_3**|**datetime**|默认值为 NULL。|  
|**user_defined_4**|**uniqueidentifier**|默认值为 NULL。|  
|**log_shipping**|**bit**|日志传送状态：<br /><br /> **0** = 已禁用**1** = 启用|  
  
  
