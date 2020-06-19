---
title: 日志传送表和存储过程 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- secondary servers [SQL Server]
- monitor servers [SQL Server]
- log shipping [SQL Server], system tables
- log shipping [SQL Server], stored procedures
- primary servers [SQL Server]
ms.assetid: 03420810-4c38-4c0c-adf0-913eb044c50a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f10a6555ed3a0c27a72c3d097cc200f21d901274
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84931168"
---
# <a name="log-shipping-tables-and-stored-procedures"></a>Log Shipping Tables and Stored Procedures
  本主题介绍与日志传送配置关联的所有表和存储过程。 所有日志传送表都存储在每个服务器的 **msdb** 中。 下表介绍在日志传送配置中，哪些服务器上使用的是哪些表和存储过程。  
  
## <a name="primary-server-tables"></a>主服务器表  
  
|表|说明|  
|-----------|-----------------|  
|[log_shipping_monitor_alert](/sql/relational-databases/system-tables/log-shipping-monitor-alert-transact-sql)|存储警报作业 ID。 仅当尚未配置远程监视服务器时，主服务器上才会使用此表。|  
|[log_shipping_monitor_error_detail](/sql/relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql)|存储与此主服务器关联的日志传送作业的错误详细信息。|  
|[log_shipping_monitor_history_detail](/sql/relational-databases/system-tables/log-shipping-monitor-history-detail-transact-sql)|存储与此主服务器关联的日志传送作业的历史记录详细信息。|  
|[log_shipping_monitor_primary](/sql/relational-databases/system-tables/log-shipping-monitor-primary-transact-sql)|存储一条此主数据库的监视记录。|  
|[log_shipping_primary_databases](/sql/relational-databases/system-tables/log-shipping-primary-databases-transact-sql)|包含指定服务器上主数据库的配置信息。 每个主数据库存储一行。|  
|[log_shipping_primary_secondaries](/sql/relational-databases/system-tables/log-shipping-primary-secondaries-transact-sql)|将主数据库映射到辅助数据库。|  
  
## <a name="primary-server-stored-procedures"></a>主服务器存储过程  
  
|存储过程|说明|  
|----------------------|-----------------|  
|[sp_add_log_shipping_primary_database](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql)|设置日志传送配置（包括备份作业、本地监视记录及远程监视记录）的主数据库。|  
|[sp_add_log_shipping_primary_secondary](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-primary-secondary-transact-sql)|向现有的主数据库添加辅助数据库名称。|  
|[sp_change_log_shipping_primary_database](/sql/relational-databases/system-stored-procedures/sp-change-log-shipping-primary-database-transact-sql)|更改主数据库设置，包括本地和远程监视记录。|  
|[sp_cleanup_log_shipping_history](/sql/relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql)|根据保持期清除本地历史记录及监视器上的历史记录。|  
|[sp_delete_log_shipping_primary_database](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-database-transact-sql)|删除主数据库的日志传送，包括备份作业以及本地和远程历史记录。|  
|[sp_delete_log_shipping_primary_secondary](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-secondary-transact-sql)|从主数据库中删除辅助数据库名称。|  
|[sp_help_log_shipping_primary_database](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql)|检索主数据库设置并显示 **log_shipping_primary_databases** 和 **log_shipping_monitor_primary** 表中的值。|  
|[sp_help_log_shipping_primary_secondary](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-primary-secondary-transact-sql)|检索主数据库的辅助数据库名称。|  
|[sp_refresh_log_shipping_monitor](/sql/relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql)|利用指定的日志传送代理的最新信息刷新监视器。|  
  
## <a name="secondary-server-tables"></a>辅助服务器表  
  
|表|说明|  
|-----------|-----------------|  
|[log_shipping_monitor_alert](/sql/relational-databases/system-tables/log-shipping-monitor-alert-transact-sql)|存储警报作业 ID。 仅当尚未配置远程监视服务器时，辅助服务器上才会使用此表。|  
|[log_shipping_monitor_error_detail](/sql/relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql)|存储与此辅助服务器关联的日志传送作业的错误详细信息。|  
|[log_shipping_monitor_history_detail](/sql/relational-databases/system-tables/log-shipping-monitor-history-detail-transact-sql)|存储与此辅助服务器关联的日志传送作业的历史记录详细信息。|  
|[log_shipping_monitor_secondary](/sql/relational-databases/system-tables/log-shipping-monitor-secondary-transact-sql)|存储与此辅助服务器关联的辅助数据库监视记录。每个辅助数据库存储一条监视记录。|  
|[log_shipping_secondary](/sql/relational-databases/system-tables/log-shipping-secondary-transact-sql)|包含指定服务器上辅助数据库的配置信息。 每个辅助 ID 存储一行。|  
|[log_shipping_secondary_databases](/sql/relational-databases/system-tables/log-shipping-secondary-databases-transact-sql)|存储指定辅助数据库的配置信息。 每个辅助数据库存储一行。|  
  
> [!NOTE]  
>  与指定主数据库位于同一个辅助服务器上的辅助数据库共享 **log_shipping_secondary** 表中的设置。 如果一个辅助数据库更改了共享设置，所有辅助数据库的设置都将更改。  
  
## <a name="secondary-server-stored-procedures"></a>辅助服务器存储过程  
  
|存储过程|说明|  
|----------------------|-----------------|  
|[sp_add_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql)|设置用于日志传送的辅助数据库。|  
|[sp_add_log_shipping_secondary_primary](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-primary-transact-sql)|为指定的主数据库设置主服务器信息，添加本地和远程监视器链接，并在辅助服务器上创建复制作业和还原作业。|  
|[sp_change_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-change-log-shipping-secondary-database-transact-sql)|更改辅助数据库设置，包括本地和远程监视记录。|  
|[sp_change_log_shipping_secondary_primary](/sql/relational-databases/system-stored-procedures/sp-change-log-shipping-secondary-primary-transact-sql)|更改辅助数据库设置，例如源目录、目标目录和文件保持期。|  
|[sp_cleanup_log_shipping_history](/sql/relational-databases/system-stored-procedures/sp-cleanup-log-shipping-history-transact-sql)|根据保持期清除本地历史记录及监视器上的历史记录。|  
|[sp_delete_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql)|删除辅助数据库、本地历史记录和远程历史记录。|  
|[sp_delete_log_shipping_secondary_primary](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-primary-transact-sql)|从辅助服务器上删除有关指定的主服务器的信息。|  
|[sp_help_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql)|从 **log_shipping_secondary**、 **log_shipping_secondary_databases**和 **log_shipping_monitor_secondary** 表中检索辅助数据库设置。|  
|[sp_help_log_shipping_secondary_primary](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-primary-transact-sql)|此存储过程将在辅助服务器上检索给定的主数据库的设置。|  
|[sp_refresh_log_shipping_monitor](/sql/relational-databases/system-stored-procedures/sp-refresh-log-shipping-monitor-transact-sql)|利用指定的日志传送代理的最新信息刷新监视器。|  
  
## <a name="monitor-server-tables"></a>监视服务器表  
  
|表|说明|  
|-----------|-----------------|  
|[log_shipping_monitor_alert](/sql/relational-databases/system-tables/log-shipping-monitor-alert-transact-sql)|存储警报作业 ID。|  
|[log_shipping_monitor_error_detail](/sql/relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql)|存储日志传送作业的错误详细信息。|  
|[log_shipping_monitor_history_detail](/sql/relational-databases/system-tables/log-shipping-monitor-history-detail-transact-sql)|存储日志传送作业的历史记录详细信息。|  
|[log_shipping_monitor_primary](/sql/relational-databases/system-tables/log-shipping-monitor-primary-transact-sql)|存储与此监视服务器关联的主数据库的监视记录。每个主数据库存储一条监视记录。|  
|[log_shipping_monitor_secondary](/sql/relational-databases/system-tables/log-shipping-monitor-secondary-transact-sql)|存储与此监视服务器关联的辅助数据库的监视记录。每个辅助数据库存储一条监视记录。|  
  
## <a name="monitor-server-stored-procedures"></a>监视服务器存储过程  
  
|存储过程|说明|  
|----------------------|-----------------|  
|[sp_add_log_shipping_alert_job](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-alert-job-transact-sql)|如果尚未创建日志传送警报作业，则创建它。|  
|[sp_delete_log_shipping_alert_job](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-alert-job-transact-sql)|如果没有关联的主数据库，则删除日志传送警报作业。|  
|[sp_help_log_shipping_alert_job](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-alert-job-transact-sql)|返回警报作业的作业 ID。|  
|[sp_help_log_shipping_monitor_primary](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-primary-transact-sql)|从 **log_shipping_monitor_primary** 表中返回指定的主数据库的监视记录。|  
|[sp_help_log_shipping_monitor_secondary](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-secondary-transact-sql)|从 **log_shipping_monitor_secondary** 表中返回指定的辅助数据库的监视记录。|  
  
  
