---
title: "sp_helpdatatypemap (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- sp_helpdatatypemap
- sp_helpdatatypemap_TSQL
helpviewer_keywords:
- sp_helpdatatypemap
ms.assetid: 800c9c65-723e-4961-a63d-327987f129f0
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d22a2c19f5824ef0a1cb5e0a145afd72492289df
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpdatatypemap-transact-sql"></a>sp_helpdatatypemap (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回有关之间的定义的数据类型映射信息[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和非-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库管理系统 (DBMS)。 此存储过程在分发服务器上的任何数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helpdatatypemap [ @source_dbms = ] 'source_dbms'   
    [ , [ @source_version = ] 'source_version' ]  
    [ , [ @source_type = ] 'source_type' ]   
    [ , [ @destination_dbms = ] 'destination_dbms' ]  
    [ , [ @destination_version = ] 'destination_version' ]  
    [ , [ @destination_type = ] 'destination_type' ]  
    [ , [ @defaults_only = ] defaults_only ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@source_dbms** =] *source_dbms*  
 从中映射数据类型的 DBMS 的名称。 *source_dbms*是**sysname**，和可以是以下值之一。  
  
|值|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|源为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库。|  
|**ORACLE**|源为 Oracle 数据库。|  
  
 [  **@source_version** =] *source_version*  
 源 DBMS 的产品版本。 *source_version*是**varchar(10)**，如果未指定，数据类型映射的所有版本的 DBMS 返回的源。 启用结果集按 DBMS 源版本进行筛选。  
  
 [  **@source_type** =] *source_type*  
 源 DBMS 中列出的数据类型。 *source_type*是**sysname**，并且如果未指定，将返回源 DBMS 中的所有数据类型映射。 启用结果集按源 DBMS 中的数据类型进行筛选。  
  
 [  **@destination_dbms**  =] *destination_dbms*  
 目标 DBMS 的名称。 *destination_dbms*是**sysname**，和可以是以下值之一。  
  
|值|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|目标为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库。|  
|**ORACLE**|目标为 Oracle 数据库。|  
|**DB2**|目标为 IBM DB2 数据库。|  
|**SYBASE**|目标为 Sybase 数据库。|  
  
 [  **@destination_version** =] *destination_version*  
 是目标 DBMS 的产品版本。 *destination_version*是**varchar(10)**，并且如果未指定，将返回有关目标 DBMS 的所有版本的映射。 启用结果集按 DBMS 的目标版本进行筛选。  
  
 [  **@destination_type** =] *destination_type*  
 目标 DBMS 中列出的数据类型。 *destination_type*是**sysname**，并且如果未指定，将返回目标 DBMS 中的所有数据类型映射。 启用结果集按目标 DBMS 中的数据类型进行筛选。  
  
 [  **@defaults_only** =] *defaults_only*  
 指示是否仅返回默认数据类型映射。 *defaults_only*是**位**，默认值为**0**。 **1**返回仅的默认数据类型映射的方式。 **0**返回默认值以及用户定义的任何数据类型映射的方式。  
  
## <a name="result-sets"></a>结果集  
  
|列名|Description|  
|-----------------|-----------------|  
|**mapping_id**|标识数据类型映射。|  
|**source_dbms**|源 DBMS 的名称和版本号。|  
|**source_type**|源 DBMS 中的数据类型。|  
|**destination_dbms**|目标 DBMS 的名称。|  
|**destination_type**|目标 DBMS 中的数据类型。|  
|**is_default**|指示映射是默认映射还是替代映射。 值为**0**指示此映射是用户定义。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_helpdatatypemap**定义数据类型映射从非 SQL Server 发布服务器和从[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布者非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]订阅服务器。  
  
 不支持源和目标 DBMS 的指定的组合， **sp_helpdatatypemap**返回空结果集。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色在分发服务器或成员的**db_owner**在分发数据库上的固定的数据库角色可以执行**sp_helpdatatypemap**.  
  
## <a name="see-also"></a>另请参阅  
 [sp_getdefaultdatatypemapping &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)   
 [sp_setdefaultdatatypemapping &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md)  
  
  
