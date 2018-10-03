---
title: sp_refresh_log_shipping_monitor (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_refresh_log_shipping_monitor
- sp_refresh_log_shipping_monitor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_refresh_log_shipping_monitor
ms.assetid: edefb912-31c5-4d99-9aba-06629afd0171
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4382dc4de4010944e60cb37640759e91a0fc2727
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47851555"
---
# <a name="sprefreshlogshippingmonitor-transact-sql"></a>sp_refresh_log_shipping_monitor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  此存储过程使用指定日志传送代理的给定主服务器或辅助服务器中的最新信息来刷新远程监视器表。 此过程将在主服务器或辅助服务器上被调用。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_refresh_log_shipping_monitor  
[ @agent_id = ] 'agent_id',  
[ @agent_type = ] 'agent_type'  
[ @database = ] 'database'  
[ @mode ] n  
```  
  
## <a name="arguments"></a>参数  
 [ **@agent_id=** ] **'***agent_id***'**  
 用于备份的主 ID 或者用于复制或还原的辅助 ID。 *agent_id*是**uniqueidentifier**且不能为 NULL。  
  
 [ **@agent_type=** ] **'***agent_type***'**  
 日志传送作业的类型。  
  
 0 = 备份。  
  
 1 = 复制。  
  
 2 = 还原。  
  
 *agent_type*是**tinyint**且不能为 NULL。  
  
 [  **@database=** ] **'***数据库*****  
 备份或还原代理进行日志记录时使用的主数据库或辅助数据库。  
  
 [ **@mode** ] *n*  
 指定是否刷新监视器数据或清除数据。 数据类型*m*为 tinyint，和支持的值为：  
  
 1 = 刷新（默认值）。  
  
 2 = 删除  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 无。  
  
## <a name="remarks"></a>备注  
 **sp_refresh_log_shipping_monitor**刷新**log_shipping_monitor_primary**， **log_shipping_monitor_secondary**， **log_shipping_monitor_history_detail**，并**log_shipping_monitor_error_detail**尚未传输任意会话信息的表。 当监视已有一段时间不同步时，您便可以使监视服务器与主服务器或辅助服务器同步。 此外，如果需要，还可以从监视服务器中清除监视信息。  
  
 **sp_refresh_log_shipping_monitor**必须从运行**主**主密钥或辅助服务器上的数据库。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色可以运行此过程。  
  
## <a name="see-also"></a>请参阅  
 [关于日志传送 (SQL Server)](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
