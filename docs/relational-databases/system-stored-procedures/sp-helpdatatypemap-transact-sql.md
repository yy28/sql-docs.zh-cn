---
title: sp_helpdatatypemap (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_helpdatatypemap
- sp_helpdatatypemap_TSQL
helpviewer_keywords:
- sp_helpdatatypemap
ms.assetid: 800c9c65-723e-4961-a63d-327987f129f0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e1eab8424e2ff5eb81e8d89a6ed897b7d19b5b72
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47837935"
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
 [ **@source_dbms**=] **'***source_dbms*****  
 从中映射数据类型的 DBMS 的名称。 *source_dbms*是**sysname**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|源为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库。|  
|**ORACLE**|源为 Oracle 数据库。|  
  
 [ **@source_version**=] **'***source_version*****  
 源 DBMS 的产品版本。 *source_version*是**varchar(10)**，并且如果未指定的数据类型将返回的源 DBMS 的所有版本的映射。 启用结果集按 DBMS 源版本进行筛选。  
  
 [ **@source_type**=] **'***source_type*****  
 源 DBMS 中列出的数据类型。 *source_type*是**sysname**，如果未指定，将返回源 DBMS 中的所有数据类型映射。 启用结果集按源 DBMS 中的数据类型进行筛选。  
  
 [ **@destination_dbms** =] **'***destination_dbms*****  
 目标 DBMS 的名称。 *destination_dbms*是**sysname**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|目标为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库。|  
|**ORACLE**|目标为 Oracle 数据库。|  
|**DB2**|目标为 IBM DB2 数据库。|  
|**SYBASE**|目标为 Sybase 数据库。|  
  
 [ **@destination_version**=] **'***destination_version*****  
 目标 DBMS 的产品版本。 *destination_version*是**varchar(10)**，如果未指定，将返回目标 DBMS 的所有版本的映射。 启用结果集按 DBMS 的目标版本进行筛选。  
  
 [ **@destination_type**=] **'***destination_type*****  
 目标 DBMS 中列出的数据类型。 *destination_type*是**sysname**，如果未指定，将返回目标 DBMS 中的所有数据类型映射。 启用结果集按目标 DBMS 中的数据类型进行筛选。  
  
 [ **@defaults_only**=] *defaults_only*  
 指示是否仅返回默认数据类型映射。 *defaults_only*是**位**，默认值为**0**。 **1**表示仅默认数据类型映射返回。 **0**表示默认值和用户定义的任何数据类型映射返回。  
  
## <a name="result-sets"></a>结果集  
  
|列名|Description|  
|-----------------|-----------------|  
|**mapping_id**|标识数据类型映射。|  
|**source_dbms**|源 DBMS 的名称和版本号。|  
|**source_type**|源 DBMS 中的数据类型。|  
|**destination_dbms**|目标 DBMS 的名称。|  
|**destination_type**|目标 DBMS 中的数据类型。|  
|**is_default**|指示映射是默认映射还是替代映射。 值为**0**指示此映射是用户定义的。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_helpdatatypemap**定义从非 SQL Server 发布服务器和从数据类型映射[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器到非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]订阅服务器。  
  
 不支持指定的源和目标 DBMS 组合，则当**sp_helpdatatypemap**返回空结果集。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色的成员的分发服务器**db_owner**上的分发数据库的固定的数据库角色可以执行**sp_helpdatatypemap**.  
  
## <a name="see-also"></a>请参阅  
 [sp_getdefaultdatatypemapping &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)   
 [sp_setdefaultdatatypemapping &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md)  
  
  
