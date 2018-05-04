---
title: sp_helpdistributiondb (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_helpdistributiondb_TSQL
- sp_helpdistributiondb
helpviewer_keywords:
- sp_helpdistributiondb
ms.assetid: a2917020-26d1-4011-99f8-9212d120fd2d
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 9d52dfc8be41dc8a86fc87803a50939f03558691
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpdistributiondb-transact-sql"></a>sp_helpdistributiondb (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回指定分发数据库的属性。 此存储过程在分发服务器上对分发数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helpdistributiondb [ [ @database= ] 'database_name' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@database=**] *****database_name*****  
 是为其返回属性的数据库的名称。 *database_name*是**sysname**，默认值为**%** 关联与分发服务器，并且在其上的所有数据库用户具有的权限。  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**sysname**|分发数据库的名称。|  
|**min_distretention**|**int**|事务被删除前的最小保持期（以小时为单位）。|  
|**max_distretention**|**int**|事务被删除前的最大保持期（以小时为单位）。|  
|**历史记录保持期**|**int**|要保留历史记录的小时数。|  
|**history_cleanup_agent**|**sysname**|历史记录清除代理的名称。|  
|**distribution_cleanup_agent**|**sysname**|分发清除代理的名称。|  
|**status**|**int**|仅限内部使用。|  
|**data_folder**|**nvarchar(255)**|用于存储数据库文件的目录的名称。|  
|**data_file**|**nvarchar(255)**|数据库文件名。|  
|**data_file_size**|**int**|以 MB 为单位的数据文件初始大小。|  
|**log_folder**|**nvarchar(255)**|数据库日志文件的目录名。|  
|**log_file**|**nvarchar(255)**|日志文件的名称。|  
|**log_file_size**|**int**|以 MB 为单位的日志文件初始大小。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_helpdistributiondb**在所有类型的复制中使用。  
  
## <a name="permissions"></a>权限  
 成员**db_owner**固定的数据库角色或**replmonitor**分发数据库中的角色和使用分发数据库的发布的发布访问列表中的用户可以执行**sp_helpdistributiondb**返回与文件相关的信息。 成员**公共**角色可以执行**sp_helpdistributiondb**可返回的它们有权访问的分发数据库文件相关的信息。  
  
## <a name="see-also"></a>另请参阅  
 [查看和修改分发服务器和发布服务器属性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistributiondb &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)   
 [sp_changedistributiondb &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md)   
 [sp_dropdistributiondb &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
