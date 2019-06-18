---
title: MSdistpublishers (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdistpublishers
- MSdistpublishers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistpublishers system table
ms.assetid: 31844099-4b33-4dc9-84b4-bac70aa82598
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b867e4ffe4b23ee1a7195bb3c201ae05c2b6d075
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62817051"
---
# <a name="msdistpublishers-transact-sql"></a>MSdistpublishers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  **MSdistpublishers**表为每个远程发布服务器支持的本地分发服务器包含一行。 此表存储中**msdb**数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**sysname**|发布服务器分发服务器的名称。|  
|**distribution_db**|**sysname**|分发数据库的名称。|  
|**working_directory**|**nvarchar(255)**|用于存储发布的数据和架构文件的工作目录的名称。|  
|**security_mode**|**int**|在分发服务器上实现的安全模式：<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。<br /><br /> **1** = Windows 身份验证。|  
|**login**|**sysname**|登录 ID[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。|  
|**password**|**nvarchar(524)**|用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证的密码（已加密）。|  
|**active**|**bit**|指示远程发布服务器是否在使用本地分发服务器。|  
|**trusted**|**bit**|指示远程发布服务器是否使用与本地分发服务器相同的密码：<br /><br /> **0** = A 密码需要远程发布服务器上，才能连接到分发服务器。<br /><br /> **1** = 不需要密码。|  
|**third_party**|**bit**|发布服务器是否为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的安装：<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装。**1** = 异类数据源。|  
|**publisher_type**|**sysname**|发布服务器类型：<br /><br /> **MSSQLSERVER**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。<br /><br /> **ORACLE** = 标准 Oracle 发布服务器。<br /><br /> **ORACLE 网关**= Oracle 网关发布服务器。|  
|**storage_connection_string**|**nvarchar(779)**|Azure SQL 数据库存储连接字符串的值。|  

  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
