---
description: sp_cleanup_log_shipping_history (Transact-SQL)
title: sp_cleanup_log_shipping_history (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cleanup_log_shipping_history_TSQL
- sp_cleanup_log_shipping_history
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cleanup_log_shipping_history
ms.assetid: 96d236a9-1d0e-4f83-a4d3-f825b7381e46
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 42edf059f077f0896cd3c62b1420658c982b3d5a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88486138"
---
# <a name="sp_cleanup_log_shipping_history-transact-sql"></a>sp_cleanup_log_shipping_history (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  此存储过程将根据保持期，清理本地和监视服务器上的历史记录。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_cleanup_log_shipping_history  
[ @agent_id = ] 'agent_id',  
[ @agent_type = ] 'agent_type'  
```  
  
## <a name="arguments"></a>参数  
`[ @agent_id = ] 'agent_id',` 用于备份的主 ID 或者用于复制或还原的辅助 ID。 *agent_id* 为 **uniqueidentifier** ，且不能为 NULL。  
  
`[ @agent_type = ] 'agent_type'` 日志传送作业的类型。 0 = 备份，1 = 复制，2 = 还原。 *agent_type* 为 **tinyint** ，且不能为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 无。  
  
## <a name="remarks"></a>备注  
 必须从任何日志传送服务器上的**master**数据库运行**sp_cleanup_log_shipping_history** 。 此存储过程将根据历史记录保持期，清理 **log_shipping_monitor_history_detail** 和 **log_shipping_monitor_error_detail** 的本地和远程副本。  
  
## <a name="permissions"></a>权限  
 只有 **sysadmin** 固定服务器角色的成员才能运行此过程。  
  
## <a name="see-also"></a>另请参阅  
 [关于日志传送 (SQL Server)](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
