---
title: core.sp_purge_data (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_purge_data_TSQL
- sp_purge_data
dev_langs:
- TSQL
helpviewer_keywords:
- sp_purge_data
- management data warehouse, data collector stored procedures
- core.sp_purge_data stored procedure
- data collector [SQL Server], stored procedures
ms.assetid: 056076c3-8adf-4f51-8a1b-ca39696ac390
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b929306a5f865defa4c264c289c4525694784c1b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="coresppurgedata-transact-sql"></a>core.sp_purge_data (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  基于保留策略从管理数据仓库中删除数据。 此过程通过 mdw_purge_data 每日执行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]对管理数据仓库的代理作业与指定的实例相关联。 可以使用此存储过程从管理数据仓库中执行数据的按需删除。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
core.sp_purge_data  
    [ [ @retention_days = ] retention_days ]  
    [ , [ @instance_name = ] 'instance_name' ]  
    [ , [ @collection_set_uid = ] 'collection_set_uid' ]  
    [ , [ @duration = ] duration ]  
```  
  
## <a name="arguments"></a>参数  
 [@retention_days =] *retention_days*  
 管理数据仓库表中的数据的保留天数。 带有时间戳早于数据*retention_days*中删除。 *retention_days*是**smallint**，默认值为 NULL。 如果指定，该值必须是正数。 为 NULL 时，core.snapshots 视图中的 valid_through 列中的值决定了符合删除条件的行。  
  
 [@instance_name =] '*instance_name*  
 收集组实例的名称。 *instance_name*是**sysname**，默认值为 NULL。  
  
 *instance_name*必须是完全限定的实例名称，其中包含计算机名称和窗体中的实例名称*computername*\\*instancename*。 为 NULL 时，使用本地服务器上的默认实例。  
  
 [@collection_set_uid = ] '*collection_set_uid*'  
 收集组的 GUID。 *collection_set_uid*是**uniqueidentifier**，默认值为 NULL。 为 NULL 时，将删除所有收集组中的限定行。 若要获取此值，请查询 syscollector_collection_sets 目录视图。  
  
 [@duration =]*持续时间*  
 清除操作应当运行的最长分钟数。 *持续时间*是**smallint**，默认值为 NULL。 如果指定，则该值必须是零或正整数。 为 NULL 时，操作将一直运行，直到删除所有符合条件的行或手动停止操作。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 此过程将基于保留期选择 core.snapshots 视图中符合删除条件的行。 符合删除条件的所有行将从 core.snapshots_internal 表中删除。 删除位于前面的行将在所有管理数据仓库表中触发级联删除操作。 通过使用 ON DELETE CASCADE 子句可以完成此操作，该子句是为用于存储收集的数据的所有表定义的。  
  
 每个快照及其关联的数据都将在显式事务中删除，然后提交。 因此，如果已手动停止该清除操作，或指定的值@duration超出，仅未提交的数据保持。 此数据可以在下一次运行作业时删除。  
  
 必须在管理数据仓库数据库的上下文中执行此过程。  
  
## <a name="permissions"></a>权限  
 要求的成员身份**mdw_admin** （拥有 EXECUTE 权限） 固定的数据库角色。  
  
## <a name="examples"></a>示例  
  
### <a name="a-running-sppurgedata-with-no-parameters"></a>A. 无参数运行 sp_purge_data  
 以下示例在不指定任何参数的情况下执行 core.sp_purge_data。 因此，默认值 NULL 及关联行为将用于所有参数。  
  
```  
USE <management_data_warehouse>;  
EXECUTE core.sp_purge_data;  
GO  
```  
  
### <a name="b-specifying-retention-and-duration-values"></a>B. 指定保留期和持续时间值  
 下面的示例从管理数据仓库中删除超过 7 天的数据。 此外，@duration参数指定，因此该操作将运行不超过 5 分钟。  
  
```  
USE <management_data_warehouse>;  
EXECUTE core.sp_purge_data @retention_days = 7, @duration = 5;  
GO  
```  
  
### <a name="c-specifying-an-instance-name-and-collection-set"></a>C. 指定实例名称和收集组  
 下面的示例从指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上的给定收集组的管理数据仓库中删除数据。 因为@retention_days未指定，则 core.snapshots 视图中的 valid_through 列中的值用于确定适合删除收集组的行。  
  
```  
USE <management_data_warehouse>;  
GO  
-- Get the collection set unique identifier for the Disk Usage system collection set.  
DECLARE @disk_usage_collection_set_uid uniqueidentifier = (SELECT collection_set_uid   
    FROM msdb.dbo.syscollector_collection_sets WHERE name = N'Disk Usage');   
  
EXECUTE core.sp_purge_data @instance_name = @@SERVERNAME, @collection_set_uid = @disk_usage_collection_set_uid;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [数据收集器存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)  
  
  
