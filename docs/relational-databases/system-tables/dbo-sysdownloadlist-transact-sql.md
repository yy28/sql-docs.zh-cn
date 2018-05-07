---
title: dbo.sysdownloadlist (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4390fe628a879b36b42ffd1a3c3209e910eb125c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="dbosysdownloadlist-transact-sql"></a>dbo.sysdownloadlist (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包含所有目标服务器的下载指令队列。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**instance_id**|**int**|对提供行的自然插入顺序的列进行标识。|  
|**source_server**|**sysname**|源服务器的名称。|  
|**operation_code**|**tinyint**|作业的操作代码：<br /><br /> **1** = INS (INSERT)<br /><br /> **2** = UPD （更新）<br /><br /> **3** = DEL (DELETE)<br /><br /> **4** = START<br /><br /> **5** = 停止|  
|**object_type**|**tinyint**|对象类型代码。|  
|**object_id** <sup>1</sup>|**uniqueidentifier**|对象标识号。|  
|**target_server**|**sysname**|目标服务器的名称。|  
|**error_message**|**nvarchar(1024)**|目标服务器处理特定行时，遇到错误时出现的错误消息。|  
|**date_posted**|**datetime**|将作业发布到目标服务器的日期和时间。|  
|**date_downloaded**|**datetime**|上次下载作业的日期和时间。|  
|**status**|**tinyint**|作业的状态：<br /><br /> **0** = 不尚未下载<br /><br /> **1** = 成功下载|  
|**deleted_object_name**|**sysname**|删除的对象的名称。|  
  
 <sup>1</sup> **object_id**列可以是值为 **-1**，对应于值为所有的 if **operation_code**列是删除的值。  
  
  
