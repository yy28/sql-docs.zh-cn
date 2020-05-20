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
ms.openlocfilehash: ea1769f7fc7e1baa58d4335c7a5ecfc99de78bb3
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82820958"
---
# <a name="mssubscriber_info-transact-sql"></a>MSsubscriber_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  对于从本地分发服务器推送的每个发布服务器/订阅服务器对， **MSsubscriber_info**表中各占一行。 此表存储在分发数据库中。  
  
 **注意**已不推荐使用此系统表，正在维护此表以支持早期版本的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="definition"></a>定义  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**器**|**sysname**|发布服务器的名称。|  
|**订阅服务器**|**sysname**|订阅服务器的名称。|  
|type |**tinyint**|订阅服务器类型：<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅服务器。<br /><br /> **1** = ODBC 数据源。|  
|**id**|**sysname**|用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证的登录名。 如果添加订阅服务器时指定的是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证模式，则以加密格式进行存储。|  
|**password**|**nvarchar （524）**|用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证的密码。 如果添加订阅服务器时指定的是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证模式，则以加密格式进行存储。|  
|**2008**|**nvarchar(255)**|订阅服务器的说明。|  
|**security_mode**|**int**|所实现的安全模式：<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证。<br /><br /> **1**个  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 身份验证。|  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;&#40;复制表](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
