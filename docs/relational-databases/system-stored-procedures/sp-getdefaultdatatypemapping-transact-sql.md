---
title: sp_getdefaultdatatypemapping (TRANSACT-SQL) |Microsoft Docs
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
- sp_getdefaultdatatypemapping_TSQL
- sp_getdefaultdatatypemapping
helpviewer_keywords:
- sp_getdefaultdatatypemapping
ms.assetid: b8401de1-f135-41d0-ba79-ce8fe1f48c00
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ff9df7e27545aa130398e0a81ffcf24855503aba
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43025706"
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
 [ **@source_dbms**=] **'***source_dbms*****  
 从中映射数据类型的 DBMS 的名称。 *source_dbms*是**sysname**，可以是下列值之一：  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|源为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库。|  
|**ORACLE**|源为 Oracle 数据库。|  
  
 必须指定此参数。  
  
 [  **@source_version=** ] **'***source_version*****  
 源 DBMS 的版本号。 *source_version*是**varchar(10)**，默认值为 NULL。  
  
 [ **@source_type**=] **'***source_type*****  
 源 DBMS 中的数据类型。 *source_type*是**sysname**，无默认值。  
  
 [  **@source_length=** ] *source_length*  
 源 DBMS 中的数据类型的长度。 *source_length*是**bigint**，默认值为 NULL。  
  
 [  **@source_precision=** ] *source_precision*  
 源 DBMS 中的数据类型的精度。 *source_precision*是**bigint**，默认值为 NULL。  
  
 [  **@source_scale=** ] *source_scale*  
 源 DBMS 中的数据类型的小数位数。 *source_scale*是**int**，默认值为 NULL。  
  
 [  **@source_nullable=** ] *source_nullable*  
 源 DBMS 中的数据类型是否支持 NULL 值。 *source_nullable*是**位**，默认值为**1**，这意味着支持 NULL 值。  
  
 [ **@destination_dbms** =] **'***destination_dbms*****  
 目标 DBMS 的名称。 *destination_dbms*是**sysname**，可以是下列值之一：  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|目标为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库。|  
|**ORACLE**|目标为 Oracle 数据库。|  
|**DB2**|目标为 IBM DB2 数据库。|  
|**SYBASE**|目标为 Sybase 数据库。|  
  
 必须指定此参数。  
  
 [ **@destination_version**=] **'***destination_version*****  
 目标 DBMS 的产品版本。 *destination_version*是**varchar(10)**，默认值为 NULL。  
  
 [ **@destination_type**=] **'***destination_type***** 输出  
 目标 DBMS 中列出的数据类型。 *destination_type*是**sysname**，默认值为 NULL。  
  
 [  **@destination_length=** ] *destination_length*输出  
 目标 DBMS 中的数据类型的长度。 *destination_length*是**bigint**，默认值为 NULL。  
  
 [  **@destination_precision=** ] *destination_precision*输出  
 目标 DBMS 中的数据类型的精度。 *destination_precision*是**bigint**，默认值为 NULL。  
  
 [  **@destination_scale=** ] *destination_scale * * * 输出**  
 目标 DBMS 中的数据类型的小数位数。 *destination_scale*是**int**，默认值为 NULL。  
  
 [  **@destination_nullable=** ] *destination_nullable * * * 输出**  
 目标 DBMS 中的数据类型是否支持 NULL 值。 *destination_nullable*是**位**，默认值为 NULL。 **1**意味着支持 NULL 值。  
  
 [  **@dataloss=** ]*数据丢失 * * * 输出**  
 映射是否有数据丢失的可能。 *数据丢失*是**位**，默认值为 NULL。 **1**意味着就可能出现数据丢失。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>Remarks  
 **sp_getdefaultdatatypemapping**用于所有类型之间的复制[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]与非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DBMS。  
  
 **sp_getdefaultdatatypemapping**返回类型与指定的源数据类型最匹配的默认目标数据。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_getdefaultdatatypemapping**。  
  
## <a name="see-also"></a>请参阅  
 [sp_helpdatatypemap &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)   
 [sp_setdefaultdatatypemapping &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md)   
 [Data Type Mapping for Oracle Publishers](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)   
 [Oracle 订阅服务器](../../relational-databases/replication/non-sql/oracle-subscribers.md)  
  
  
