---
title: "sp_helpmergepartition (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helpmergepartition
- sp_helpmergepartition_TSQL
helpviewer_keywords:
- sp_helpmergepartition
ms.assetid: 184188cc-f519-445d-97ce-aae38f1eb550
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a2c4e931f2da9794392056595ab71b88e005a26f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpmergepartition-transact-sql"></a>sp_helpmergepartition (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回指定合并发布的分区信息。 此存储过程在发布服务器的任何数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helpmergepartition [ @publication= ] 'publication'   
    [ , [ @suser_sname = ] 'suser_sname' ]  
    [ , [ @host_name = ] 'host_name' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@publication=** ] *发布*  
 发布的名称。 *发布*是**sysname**，无默认值。  
  
 [  **@suser_sname=** ] *suser_sname*  
 用于定义分区的 SUSER_SNAME 值。 *suser_sname*是**sysname**，默认值为 NULL。 提供此参数是为了将结果集限制在仅将 SUSER_SNAME 解析为提供的值的分区中。  
  
> [!NOTE]  
>  当*suser_sname*提供，则*host_name*必须为 NULL  
  
 [  **@host_name=** ] *host_name*  
 用于定义分区的 HOST_NAME 值。 *host_name*是**sysname**，默认值为 NULL。 提供此参数是为了将结果集限制在仅将 HOST_NAME 解析为提供的值的分区中。  
  
> [!NOTE]  
>  当*suser_sname*提供，则*host_name*必须为 NULL  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**分区**|**int**|标识订阅服务器分区。|  
|**host_name**|**sysname**|创建订阅分区来进行筛选的值时所用值[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)订阅服务器上的函数。|  
|**suser_sname**|**sysname**|创建订阅分区来进行筛选的值时所用值[SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md)订阅服务器上的函数。|  
|**dynamic_snapshot_location**|**nvarchar(255)**|订阅服务器分区的已筛选数据快照的位置。|  
|**date_refreshed**|**datetime**|最近运行快照作业为分区生成已筛选数据快照的日期。|  
|**dynamic_snapshot_jobid**|**uniqueidentifier**|标识为分区创建已筛选数据快照的作业。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_helpmergepartition**合并复制中使用。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色和**db_owner**固定的数据库角色可以执行**sp_helpmergepartition**。  
  
## <a name="see-also"></a>另请参阅  
 [sp_addmergepartition &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md)   
 [sp_dropmergepartition &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropmergepartition-transact-sql.md)  
  
  
