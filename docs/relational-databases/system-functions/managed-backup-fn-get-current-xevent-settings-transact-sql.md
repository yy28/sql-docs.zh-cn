---
title: managed_backup.fn_get_current_xevent_settings (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_get_current_xevent_settings
- smart_admin.fn_get_current_xevent_settings_TSQL
- fn_get_current_xevent_settings_TSQL
- smart_admin.fn_get_current_xevent_settings
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.fn_get_current_xevent_settings
- fn_get_current_xevent_settings
ms.assetid: 95d3adaa-bb9d-4833-b8b4-3d9fd4f9c82a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4133f8bb64d5d7e2e2b511c2128b9ddbca1fa550
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67910247"
---
# <a name="managedbackupfngetcurrentxeventsettings-transact-sql"></a>managed_backup.fn_get_current_xevent_settings (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  为智能管理支持的每个扩展事件类型返回 1 行。  
  
 使用此函数可返回或查看当前的扩展事件设置，以识别可配置事件的类型以及当前的配置。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```sql  
smart_admin.fn_get_current_xevent_settings ()   
```  
  
##  <a name="Arguments"></a> 参数  
 此函数没有任何参数。  
  
## <a name="table-returned"></a>返回的表  
 默认情况下必须启用扩展事件的管理、分析和运行通道，并且不可配置这些通道。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|Event_name|NVARCHAR(128)|扩展事件类型|  
|is_configurable|NVARCHAR(128)|此值设置为 **，则返回 True**如果事件是可配置，否则它设置为**False**。|  
|is_enabled|NVARCHAR(128)|如果启用了事件，则此项设置为 True；否则设置为 False。 使用 smart_admin.sp_set_parameter 启用调试事件。|  
  
## <a name="security"></a>安全性  
  
### <a name="permissions"></a>权限  
 需要**选择**函数上的权限。  
  
## <a name="examples"></a>示例  
 以下示例返回所有扩展事件及其当前的状态。  
  
```  
SELECT *   
FROM smart_admin.fn_get_current_xevent_settings ()  
  
```  
  
  
