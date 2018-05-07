---
title: MSdistpublishers (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSdistpublishers
- MSdistpublishers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistpublishers system table
ms.assetid: 31844099-4b33-4dc9-84b4-bac70aa82598
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 2565f080af7fc798a4f53cdaa425387b75652d2b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="msdistpublishers-transact-sql"></a>MSdistpublishers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  **MSdistpublishers**表为每个支持的本地分发服务器的远程发布服务器包含一个行。 此表存储在**msdb**数据库。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**sysname**|发布服务器分发服务器的名称。|  
|**distribution_db**|**sysname**|分发数据库的名称。|  
|**working_directory**|**nvarchar(255)**|用于存储数据和架构文件为发布的工作目录的名称。|  
|**security_mode**|**int**|在分发服务器上实现的安全模式：<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。<br /><br /> **1** = Windows 身份验证。|  
|**login**|**sysname**|登录 ID 的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。|  
|**password**|**nvarchar(524)**|用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证的密码（已加密）。|  
|**活动**|**bit**|指示远程发布服务器是否在使用本地分发服务器。|  
|**受信任**|**bit**|指示远程发布服务器是否使用与本地分发服务器相同的密码：<br /><br /> **0** = A 密码需要在远程发布服务器连接到分发服务器。<br /><br /> **1** = 否，就需要密码。|  
|**third_party**|**bit**|发布服务器是否为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的安装：<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装。**1** = 异类数据源。|  
|**publisher_type**|**sysname**|发布服务器类型：<br /><br /> **MSSQLSERVER**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。<br /><br /> **ORACLE** = 标准 Oracle 发布服务器。<br /><br /> **ORACLE 网关**= Oracle 网关发布服务器。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
