---
title: sp_change_log_shipping_secondary_database （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: d0bd62fe3462441d4eab9d3d89bce20cf1144131
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909558"
---
# <a name="sp_change_log_shipping_secondary_database-transact-sql"></a>sp_change_log_shipping_secondary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改辅助数据库设置。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [transact-sql 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @restore_delay = ] 'restore_delay'` 在还原给定备份文件之前辅助服务器等待的时间，以分钟为单位。 *restore_delay*的值为**int** ，且不能为 NULL。 默认值为 0。  
  
`[ @restore_all = ] 'restore_all'` 如果设置为1，辅助服务器将在还原作业运行时还原所有可用的事务日志备份。 否则，在原还了一个文件之后它将停止。 *restore_all*为**bit** ，并且不能为 NULL。  
  
`[ @restore_mode = ] 'restore_mode'` 辅助数据库的还原模式。  
  
 0 = 使用 NORECOVERY 还原日志。  
  
 1 = 用备用还原日志。  
  
 *restore*为**bit** ，并且不能为 NULL。  
  
`[ @disconnect_users = ] 'disconnect_users'` 如果设置为1，则在执行还原操作时，用户将与辅助数据库断开连接。 默认值 = 0。 *disconnect_users*为**bit** ，并且不能为 NULL。  
  
`[ @block_size = ] 'block_size'` 用作备份设备的块大小的大小（以字节为单位）。 *block_size*的值为**int** ，默认值为-1。  
  
`[ @buffer_count = ] 'buffer_count'` 备份或还原操作使用的缓冲区总数。 *buffer_count*的值为**int** ，默认值为-1。  
  
`[ @max_transfer_size = ] 'max_transfer_size'` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 向备份设备发出的最大输入或输出请求的大小（以字节为单位）。 *max_transfersize*的值为**int** ，可以为 NULL。  
  
`[ @restore_threshold = ] 'restore_threshold'` 在生成警报之前在还原操作之间允许等待的分钟数。 *restore_threshold*的值为**int** ，且不能为 NULL。  
  
`[ @threshold_alert = ] 'threshold_alert'` 是在超过还原阈值时引发的警报。 *threshold_alert*的值为**int**，默认值为14420。  
  
`[ @threshold_alert_enabled = ] 'threshold_alert_enabled'` 指定超出*restore_threshold*时是否引发警报。 1 = 启用；0 = 禁用。 *threshold_alert_enabled*为**bit** ，并且不能为 NULL。  
  
`[ @history_retention_period = ] 'history_retention_period'` 是将保留历史记录的时间长度（以分钟为单位）。 *history_retention_period*为**int**。如果未指定值1440，则将使用该值。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>注释  
 必须从辅助服务器上的**master**数据库运行**sp_change_log_shipping_secondary_database** 。 此存储过程执行以下操作：  
  
1.  根据需要更改**log_shipping_secondary_database**记录中的设置。  
  
2.  必要时，使用提供的参数更改辅助服务器上**log_shipping_monitor_secondary**中的本地监视器记录。  

## <a name="permissions"></a>Permissions  
 只有**sysadmin**固定服务器角色的成员才能运行此过程。  
  
## <a name="examples"></a>示例  
 此示例演示如何使用**sp_change_log_shipping_secondary_database**来更新数据库**LogShipAdventureWorks**的辅助数据库参数。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [关于日志传送 (SQL Server)](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
