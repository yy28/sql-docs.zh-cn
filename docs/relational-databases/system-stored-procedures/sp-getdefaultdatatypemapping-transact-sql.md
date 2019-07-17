---
title: sp_getdefaultdatatypemapping (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_getdefaultdatatypemapping_TSQL
- sp_getdefaultdatatypemapping
helpviewer_keywords:
- sp_getdefaultdatatypemapping
ms.assetid: b8401de1-f135-41d0-ba79-ce8fe1f48c00
author: stevestein
ms.author: sstein
ms.openlocfilehash: 32fe9edf5c3d8621046a27937d83f642b1689d1a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68123987"
---
# <a name="spgetdefaultdatatypemapping-transact-sql"></a>sp_getdefaultdatatypemapping (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回指定的数据类型之间的默认映射的信息[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]与非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库管理系统 (DBMS)。 此存储过程在分发服务器上的任何数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_getdefaultdatatypemapping [ @source_dbms = ] 'source_dbms'   
    [ , [ @source_version = ] 'source_version' ]  
        , [ @source_type = ] 'source_type'    
    [ , [ @source_length = ] source_length ]  
    [ , [ @source_precision = ] source_precision ]  
    [ , [ @source_scale = ] source_scale ]  
    [ , [ @source_nullable = ] source_nullable ]  
        , [ @destination_dbms = ] 'destination_dbms'   
    [ , [ @destination_version = ] 'destination_version' ]  
    [ , [ @destination_type = ] 'destination_type' OUTPUT ]  
    [ , [ @destination_length = ] destination_length OUTPUT ]  
    [ , [ @destination_precision = ] destination_precision OUTPUT ]  
    [ , [ @destination_scale = ] destination_scale OUTPUT ]  
    [ , [ @destination_nullable = ] source_nullable OUTPUT ]  
    [ , [ @dataloss = ] dataloss OUTPUT ]  
```  
  
## <a name="arguments"></a>参数  
`[ @source_dbms = ] 'source_dbms'` 是从中映射数据类型的 DBMS 的名称。 *source_dbms*是**sysname**，可以是下列值之一：  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**MSSQLSERVER**|源为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库。|  
|**ORACLE**|源为 Oracle 数据库。|  
  
 必须指定此参数。  
  
`[ @source_version = ] 'source_version'` 是源 DBMS 的版本号。 *source_version*是**varchar(10)** ，默认值为 NULL。  
  
`[ @source_type = ] 'source_type'` 源 DBMS 中的数据类型。 *source_type*是**sysname**，无默认值。  
  
`[ @source_length = ] source_length` 是源 DBMS 中的数据类型的长度。 *source_length*是**bigint**，默认值为 NULL。  
  
`[ @source_precision = ] source_precision` 源 DBMS 中的数据类型的精度。 *source_precision*是**bigint**，默认值为 NULL。  
  
`[ @source_scale = ] source_scale` 源 DBMS 中的数据类型的小数位数。 *source_scale*是**int**，默认值为 NULL。  
  
`[ @source_nullable = ] source_nullable` 在源 DBMS 中的数据类型支持的值为 NULL。 *source_nullable*是**位**，默认值为**1**，这意味着支持 NULL 值。  
  
`[ @destination_dbms = ] 'destination_dbms'` 是目标 DBMS 的名称。 *destination_dbms*是**sysname**，可以是下列值之一：  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**MSSQLSERVER**|目标为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库。|  
|**ORACLE**|目标为 Oracle 数据库。|  
|**DB2**|目标为 IBM DB2 数据库。|  
|**SYBASE**|目标为 Sybase 数据库。|  
  
 必须指定此参数。  
  
`[ @destination_version = ] 'destination_version'` 目标 DBMS 的产品版本。 *destination_version*是**varchar(10)** ，默认值为 NULL。  
  
`[ @destination_type = ] 'destination_type' OUTPUT` 目标 DBMS 中列出的数据类型。 *destination_type*是**sysname**，默认值为 NULL。  
  
`[ @destination_length = ] destination_length OUTPUT` 是目标 DBMS 中的数据类型的长度。 *destination_length*是**bigint**，默认值为 NULL。  
  
`[ @destination_precision = ] destination_precision OUTPUT` 目标 DBMS 中的数据类型的精度。 *destination_precision*是**bigint**，默认值为 NULL。  
  
`[ @destination_scale = ] _destination_scaleOUTPUT` 目标 DBMS 中的数据类型的小数位数。 *destination_scale*是**int**，默认值为 NULL。  
  
`[ @destination_nullable = ] _destination_nullableOUTPUT` 在目标 DBMS 中的数据类型支持的值为 NULL。 *destination_nullable*是**位**，默认值为 NULL。 **1**意味着支持 NULL 值。  
  
`[ @dataloss = ] _datalossOUTPUT` 是映射是否有数据丢失的可能性。 *数据丢失*是**位**，默认值为 NULL。 **1**意味着就可能出现数据丢失。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_getdefaultdatatypemapping**用于所有类型之间的复制[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]与非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DBMS。  
  
 **sp_getdefaultdatatypemapping**返回类型与指定的源数据类型最匹配的默认目标数据。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_getdefaultdatatypemapping**。  
  
## <a name="see-also"></a>请参阅  
 [sp_helpdatatypemap &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)   
 [sp_setdefaultdatatypemapping &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md)   
 [Data Type Mapping for Oracle Publishers](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)   
 [Oracle 订阅服务器](../../relational-databases/replication/non-sql/oracle-subscribers.md)  
  
  
