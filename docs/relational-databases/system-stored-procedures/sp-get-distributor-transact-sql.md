---
title: sp_get_distributor (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_get_distributor
- sp_get_distributor_TSQL
helpviewer_keywords:
- sp_get_distributor
ms.assetid: f0134448-bc17-4f2f-bd81-619351ce56ac
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 088b2d2c6e334d48fae3e9257f76c5fd8129c15d
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43021286"
---
# <a name="spgetdistributor-transact-sql"></a>sp_get_distributor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  确定服务器上是否已安装分发服务器。 该存储过程在正在查找的分发服务器所在的计算机中的任何数据库上执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_get_distributor   
```  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**安装**|**int**|**0** = 否;**1** = yes|  
|**分发服务器**|**sysname**|分发服务器名|  
|**安装的分发数据库**|**int**|**0** = 否;**1** = yes|  
|**为分发发布服务器**|**int**|**0** = 否;**1** = yes|  
|**具有远程分发发布服务器**|**int**|**0** = 否;**1** = yes|  
  
## <a name="remarks"></a>Remarks  
 **sp_get_distributor**主要由[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]快照、 事务和合并复制。  
  
## <a name="permissions"></a>Permissions  
 任何用户都可以执行**sp_get_distributor**。 一个非 NULL 结果集返回时，此存储过程执行的成员**db_owner**或**replmonitor**固定数据库角色的成员的分发数据库上**db_owner**上至少一个已发布的数据库的固定的数据库角色。 一个非 NULL 结果集时也会返回此存储的过程执行中的发布访问列表 (PAL) 的用户在至少一个已发布数据库，或在分发数据库的非 SQL Server 发布服务器的 PAL，也可以执行**sp_get_distributor**。  
  
## <a name="see-also"></a>请参阅  
 [配置发布和分发](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [分发服务器和发布服务器信息脚本](../../relational-databases/replication/administration/distributor-and-publisher-information-script.md)   
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
