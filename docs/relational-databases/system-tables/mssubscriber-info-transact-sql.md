---
title: MSsubscriber_info （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsubscriber_info_TSQL
- MSsubscriber_info
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscriber_info system table
ms.assetid: 5ca22f41-6020-4f72-8110-e69baf3447cb
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 454b3504db5c159135d257229bb24581a254cd77
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85889386"
---
# <a name="mssubscriber_info-transact-sql"></a>MSsubscriber_info (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  对于从本地分发服务器推送的每个发布服务器/订阅服务器对， **MSsubscriber_info**表中各占一行。 此表存储在分发数据库中。  
  
 **注意**已不推荐使用此系统表，正在维护此表以支持早期版本的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="definition"></a>定义  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|发布服务器的名称。|  
|**订阅服务器**|**sysname**|订阅服务器的名称。|  
|**type**|**tinyint**|订阅服务器类型：<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅服务器。<br /><br /> **1** = ODBC 数据源。|  
|**id**|**sysname**|用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证的登录名。 如果添加订阅服务器时指定的是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证模式，则以加密格式进行存储。|  
|**password**|**nvarchar （524）**|用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证的密码。 如果添加订阅服务器时指定的是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证模式，则以加密格式进行存储。|  
|**2008**|**nvarchar(255)**|订阅服务器的说明。|  
|**security_mode**|**int**|所实现的安全模式：<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证。<br /><br /> **1**个  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 身份验证。|  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;&#40;复制表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
