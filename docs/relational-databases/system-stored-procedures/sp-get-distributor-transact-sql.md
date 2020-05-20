---
title: sp_get_distributor （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_get_distributor
- sp_get_distributor_TSQL
helpviewer_keywords:
- sp_get_distributor
ms.assetid: f0134448-bc17-4f2f-bd81-619351ce56ac
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0e714018ed35a7b6c12c0c00bd8eeffda5630b67
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82833246"
---
# <a name="sp_get_distributor-transact-sql"></a>sp_get_distributor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  确定服务器上是否已安装分发服务器。 该存储过程在正在查找的分发服务器所在的计算机中的任何数据库上执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_get_distributor   
```  
  
## <a name="result-sets"></a>结果集  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**随**|**int**|**0** = 否;**1** = 是|  
|**分发服务器**|**sysname**|分发服务器名|  
|**已安装分发数据库**|**int**|**0** = 否;**1** = 是|  
|**is distribution publisher**|**int**|**0** = 否;**1** = 是|  
|**具有远程分发发布服务器**|**int**|**0** = 否;**1** = 是|  
  
## <a name="remarks"></a>备注  
 **sp_get_distributor**主要由 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在快照复制、事务复制和合并复制中使用。  
  
## <a name="permissions"></a>权限  
 任何用户都可以执行**sp_get_distributor**。 如果此存储过程由分发数据库上**db_owner**或**replmonitor**固定数据库角色的成员或至少一个已发布数据库中**db_owner**固定数据库角色的成员执行，则将返回一个非 NULL 结果集。 如果此存储过程由至少一个已发布数据库的发布访问列表（PAL）中的用户执行，或者在非 SQL Server 发布服务器的分发数据库的 PAL 中执行此存储过程，则还会返回一个非 NULL 结果集，也可执行**sp_get_distributor**。  
  
## <a name="see-also"></a>另请参阅  
 [配置发布和分发](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [分发服务器和发布服务器信息脚本](../../relational-databases/replication/administration/distributor-and-publisher-information-script.md)   
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
