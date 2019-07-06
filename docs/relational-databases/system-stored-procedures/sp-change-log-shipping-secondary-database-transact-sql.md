---
title: sp_change_log_shipping_secondary_database (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_change_log_shipping_secondary_database
- sp_change_log_shipping_secondary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_log_shipping_secondary_database
ms.assetid: 3ebcf2f1-980f-4543-a84b-fbaeea54eeac
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5af98bd479738785c341b2618561eaab3f43b5d1
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2019
ms.locfileid: "67586021"
---
# <a name="spchangelogshippingsecondarydatabase-transact-sql"></a>sp_change_log_shipping_secondary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改辅助数据库设置。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_change_log_shipping_secondary_database  
[ @secondary_database = ] 'secondary_database',  
[, [ @restore_delay = ] 'restore_delay']  
[, [ @restore_all = ] 'restore_all']  
[, [ @restore_mode = ] 'restore_mode']  
[, [ @disconnect_users = ] 'disconnect_users']  
[, [ @block_size = ] 'block_size']  
[, [ @buffer_count = ] 'buffer_count']  
[, [ @max_transfer_size = ] 'max_transfer_size']  
[, [ @restore_threshold = ] 'restore_threshold']   
[, [ @threshold_alert = ] 'threshold_alert']   
[, [ @threshold_alert_enabled = ] 'threshold_alert_enabled']   
[, [ @history_retention_period = ] 'history_retention_period']  
```  
  
## <a name="arguments"></a>参数  
`[ @restore_delay = ] 'restore_delay'` 在辅助服务器还原给定备份文件之前等待的分钟的时间量。 *restore_delay*是**int**且不能为 NULL。 默认值为 0。  
  
`[ @restore_all = ] 'restore_all'` 如果设置为 1，辅助服务器还原所有可用的事务日志备份还原作业运行时。 否则，在原还了一个文件之后它将停止。 *restore_all*是**位**且不能为 NULL。  
  
`[ @restore_mode = ] 'restore_mode'` 辅助数据库的还原模式。  
  
 0 = 使用 NORECOVERY 还原日志。  
  
 1 = 使用 STANDBY 还原日志。  
  
 *还原*是**位**且不能为 NULL。  
  
`[ @disconnect_users = ] 'disconnect_users'` 如果执行还原操作时，设置为 1，用户已从辅助数据库断开连接。 默认值 = 0。 *disconnect_users*是**位**且不能为 NULL。  
  
`[ @block_size = ] 'block_size'` 大小 （字节），用作备份设备的块大小。 *block_size*是**int**与默认值为-1。  
  
`[ @buffer_count = ] 'buffer_count'` 使用备份或还原操作的缓冲区的总数。 *buffer_count*是**int**与默认值为-1。  
  
`[ @max_transfer_size = ] 'max_transfer_size'` 大小，以字节为单位的最大输入或输出请求发出[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]向备份设备。 *max_transfersize*是**int** ，可以为 NULL。  
  
`[ @restore_threshold = ] 'restore_threshold'` 之间允许等待的分钟数还原操作，就会生成警报。 *restore_threshold*是**int**且不能为 NULL。  
  
`[ @threshold_alert = ] 'threshold_alert'` 是要在超过还原阈值时引发的警报。 *threshold_alert*是**int**，默认值为 14420。  
  
`[ @threshold_alert_enabled = ] 'threshold_alert_enabled'` 指定是否将是警报时引发*restore_threshold*超出。 1 = 启用；0 = 禁用。 *threshold_alert_enabled*是**位**且不能为 NULL。  
  
`[ @history_retention_period = ] 'history_retention_period'` 是以分钟为单位保留历史记录长度。 *history_retention_period*是**int**。如果未指定，将使用值为 1440年。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="remarks"></a>备注  
 **sp_change_log_shipping_secondary_database**必须从运行**主**辅助服务器上的数据库。 此存储过程执行以下操作：  
  
1.  更改中的设置**log_shipping_secondary_database**记录。  
  
2.  更改在本地监视记录**log_shipping_monitor_secondary**辅助服务器上使用提供的参数，如有必要。  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以运行此过程。  
  
## <a name="examples"></a>示例  
 此示例演示如何使用**sp_change_log_shipping_secondary_database**用于更新数据库的辅助数据库参数**LogShipAdventureWorks**。  
  
```  
EXEC master.dbo.sp_change_log_shipping_secondary_database   
 @secondary_database =  'LogShipAdventureWorks'  
,  @restore_delay = 0  
,  @restore_all = 1  
,  @restore_mode = 0  
,  @disconnect_users = 0  
,  @threshold_alert = 14420  
,  @threshold_alert_enabled = 1  
,  @history_retention_period = 14420;  
```  
  
## <a name="see-also"></a>请参阅  
 [关于日志传送 (SQL Server)](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
