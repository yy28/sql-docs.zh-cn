---
title: core.sp_update_data_source (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/03/2017
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
- sp_update_data_source
- sp_update_data_source_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_data_source
- management data warehouse, data collector stored procedures
- core.sp_update_data_source stored procedure
- data collector [SQL Server], stored procedures
ms.assetid: 66b95f96-6df7-4657-9b3c-86a58c788ca5
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 042f03a9004a357e0b7a488494533d7f778247b9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="corespupdatedatasource-transact-sql"></a>core.sp_update_data_source (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更新管理数据仓库 core.source_info_internal 表中的现有行或在其中插入新行。 每次上载包开始将数据上载到管理数据仓库时，数据收集器运行时组件都会调用此过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
core.sp_update_data_source [ @collection_set_uid = ] 'collection_set_uid'  
    ,[ @machine_name = ] 'machine_name'  
    , [ @named_instance = ] 'named_instance'  
    , [ @days_until_expiration = ] days_until_expiration  
    , [ @source_id = ] source_id OUTPUT  
```  
  
## <a name="arguments"></a>参数  
 [ @collection_set_uid = ] '*collection_set_uid*'  
 收集组的 GUID。 *collection_set_uid*是**uniqueidentifier**，无默认值。 若要获取 GUID，请查询 msdb 数据库中的 dbo.syscollector_collection_sets 视图。  
  
 [ @machine_name =] '*machine_name*  
 收集组所在的服务器的名称。 *machine_name*是**sysname**无默认值。  
  
 [ @named_instance =] '*named_instance*  
 收集组实例的名称。 *named_instance*是**sysname**，无默认值。  
  
> [!NOTE]  
>  *named_instance*必须是完全限定的实例名称，其中包含计算机名称和窗体中的实例名称*computername*\\*instancename*。  
  
 [ @days_until_expiration = ] *days_until_expiration*  
 快照数据保持期剩余天数。 *days_until_expiration*是**smallint**。  
  
 [ @source_id = ] *source_id*  
 更新的来源的唯一标识符。 *source_id*是**int**和返回作为输出。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 每当上载包开始向管理数据仓库上载数据时，数据收集器运行时组件都会调用 core.sp_update_data_source。 如果自上次上载后发生了以下某项更改，则更新 core.source_info_internal 表：  
  
-   添加了新收集组。  
  
-   days_until_expiration 的值已更改。  
  
## <a name="permissions"></a>权限  
 要求的成员身份**mdw_writer** （拥有 EXECUTE 权限） 固定的数据库角色。  
  
## <a name="examples"></a>示例  
 下面的示例更新数据源（在本例中为“磁盘使用情况”收集组）、设置过期前的天数并返回数据源的标识符。 在本示例中，使用默认实例。  
  
```  
USE <management_data_warehouse>;  
GO  
DECLARE @source_id int;  
EXEC core.sp_update_data_source   
@collection_set_uid = '7B191952-8ECF-4E12-AEB2-EF646EF79FEF',   
@machine_name = '<computername>',  
@named_instance = 'MSSQLSERVER',  
@days_until_expiration = 10,  
@source_id = @source_id OUTPUT;  
```  
  
## <a name="see-also"></a>另请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [数据收集器存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [管理数据仓库](../../relational-databases/data-collection/management-data-warehouse.md)  
  
  
