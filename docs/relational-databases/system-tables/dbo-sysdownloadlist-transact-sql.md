---
title: dbo.sysdownloadlist (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysdownloadlist
- sysdownloadlist_TSQL
- dbo.sysdownloadlist_TSQL
- sysdownloadlist
dev_langs:
- TSQL
helpviewer_keywords:
- sysdownloadlist system table
ms.assetid: 71087a4c-e829-488e-aa7d-a9476e2b4779
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d0568403cb7f5bdf48d9be33e1b40f0be3fc1c33
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47745077"
---
# <a name="dbosysdownloadlist-transact-sql"></a>dbo.sysdownloadlist (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含所有目标服务器的下载指令队列。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**instance_id**|**int**|对提供行的自然插入顺序的列进行标识。|  
|**source_server**|**sysname**|源服务器的名称。|  
|**operation_code**|**tinyint**|作业的操作代码：<br /><br /> **1** = INS (INSERT)<br /><br /> **2** = UPD （更新）<br /><br /> **3** = DEL (DELETE)<br /><br /> **4** = 开始<br /><br /> **5** = 停止|  
|**object_type**|**tinyint**|对象类型代码。|  
|**object_id** <sup>1</sup>|**uniqueidentifier**|对象标识号。|  
|**target_server**|**sysname**|目标服务器的名称。|  
|**error_message**|**nvarchar(1024)**|目标服务器处理特定行时，遇到错误时出现的错误消息。|  
|**date_posted**|**datetime**|将作业发布到目标服务器的日期和时间。|  
|**date_downloaded**|**datetime**|上次下载作业的日期和时间。|  
|**status**|**tinyint**|作业的状态：<br /><br /> **0** = 尚未下载<br /><br /> **1** = 成功下载|  
|**deleted_object_name**|**sysname**|删除的对象的名称。|  
  
 <sup>1</sup> **object_id**列的值可以 **-1**，这对应于值所有如果**operation_code**列的值为删除。  
  
  
