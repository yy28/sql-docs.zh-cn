---
title: sp_addmergepartition (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepartition
- sp_addmergepartition_TSQL
helpviewer_keywords:
- sp_addmergepartition
ms.assetid: 02a5f46b-e5ff-4932-a3ff-7f0fd82d0981
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5599370f892d174336411573883e2feffa27b886
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58492646"
---
# <a name="spaddmergepartition-transact-sql"></a>sp_addmergepartition (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  创建订阅筛选的值的动态筛选的分区[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)或[SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md)订阅服务器上。 此存储过程是在发布服务器上发布的数据库中执行的，用于手动生成分区。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addmergepartition [ @publication = ] 'publication'  
        , [ @suser_sname = ] 'suser_sname'  
        , [ @host_name = ] 'host_name'  
```  
  
## <a name="arguments"></a>参数  
`[ @publication = ] 'publication'` 是在其创建分区的合并发布。 *发布*是**sysname**，无默认值。 如果*suser_sname*指定的值*主机名*必须为 NULL。  
  
`[ @suser_sname = ] 'suser_sname'` 使用创建分区的订阅进行筛选的值时的值[SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md)订阅服务器上的函数。 *suser_sname*是**sysname**，无默认值。  
  
`[ @host_name = ] 'host_name'` 使用创建分区的订阅进行筛选的值时的值[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)订阅服务器上的函数。 *host_name*是**sysname**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_addmergepartition**合并复制中使用。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_MergeDynamicPubPlusPartition](../../relational-databases/replication/codesnippet/tsql/sp-addmergepartition-tra_1.sql)]  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_addmergepartition**。  
  
## <a name="see-also"></a>请参阅  
 [为带有参数化筛选器的合并发布创建快照](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)   
 [参数化行筛选器](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
  
  
