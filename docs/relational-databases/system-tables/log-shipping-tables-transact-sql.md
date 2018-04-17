---
title: 日志传送表 (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- log shipping [SQL Server], system tables
- system tables [SQL Server], log shipping
ms.assetid: f8910aae-2013-4645-880c-134577cbcbe0
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: db69c2acda2deb1b21dba627f8fac3c0a86628cb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="log-shipping-tables-transact-sql"></a>日志传送表 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  以下主题介绍存储使用日志传送操作的信息的系统表。  
  
## <a name="in-this-section"></a>本節內容  
 [log_shipping_monitor_alert](../../relational-databases/system-tables/log-shipping-monitor-alert-transact-sql.md)  
 存储日志传送的警报作业 ID。  
  
 [log_shipping_monitor_error_detail](../../relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql.md)  
 存储日志传送作业的错误详细信息。  
  
 [log_shipping_monitor_history_detail](../../relational-databases/system-tables/log-shipping-monitor-history-detail-transact-sql.md)  
 存储日志传送作业的历史记录详细信息。  
  
 [log_shipping_monitor_primary](../../relational-databases/system-tables/log-shipping-monitor-primary-transact-sql.md)  
 在每个日志传送配置中为每个主数据库存储一条监视记录。  
  
 [log_shipping_monitor_secondary](../../relational-databases/system-tables/log-shipping-monitor-secondary-transact-sql.md)  
 在日志传送配置中为每个辅助数据库存储一条监视记录。  
  
 [log_shipping_primary_databases](../../relational-databases/system-tables/log-shipping-primary-databases-transact-sql.md)  
 在日志传送配置中为主数据库存储一条记录。  
  
 [log_shipping_primary_secondaries](../../relational-databases/system-tables/log-shipping-primary-secondaries-transact-sql.md)  
 将每个主数据库映射到其辅助数据库。  
  
 [log_shipping_secondary](../../relational-databases/system-tables/log-shipping-secondary-transact-sql.md)  
 为每个辅助 ID 存储一条记录。  
  
 [log_shipping_secondary_databases](../../relational-databases/system-tables/log-shipping-secondary-databases-transact-sql.md)  
 在日志传送配置中为每个辅助数据库存储一条记录。  
  
  
