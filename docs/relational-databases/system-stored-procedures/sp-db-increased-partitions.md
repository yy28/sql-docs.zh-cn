---
title: "sp_db_increased_partitions |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_db_increased_partitions_TSQL
- sp_db_increased_partitions
dev_langs: TSQL
helpviewer_keywords: sp_db_increased_partitions
ms.assetid: a8c043ec-b504-4929-ac0e-8babaa99d989
caps.latest.revision: "9"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5266ce8c25465b6fd398111e7fd7e2d6634f5f34
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spdbincreasedpartitions"></a>sp_db_increased_partitions
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  对指定的数据库启用或禁用对多达 15000 个分区的支持。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
||  
|-|  
|**适用于**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过 SP2 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP1 和更高版本)。 有关详细信息，请参阅[15,000 个分区在 SQL Server 2008 SP2 和 SQL Server 2008 R2 SP1 中支持](http://go.microsoft.com/fwlink/p/?LinkId=299658)，|  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_dp_increased_partitions   
[ @dbname ] = 'database_name'   
[ , [ @increased_partitions = ] 'increased_partitions' ] [;]  
```  
  
## <a name="arguments"></a>参数  
 [ @dbname=] '*database_name*  
 数据库的名称。 *dbname*是**sysname**默认值为 NULL。 如果*dbname*未指定，则使用当前数据库。  
  
 [ @increased_partitions=] '*increased_partitions*  
 对指定的数据库启用或禁用对 15000 个分区的支持。 *increased_partitions*是**varchar(6)**默认值为 NULL。 要启用支持，则接受的值是“ON”或“TRUE”；要禁用支持，则接受的值为“OFF”和“FALSE”。 如果*increased_partitions*未指定，则该过程返回 1，表示为指定的数据库启用了支持或 0 来指示支持处于禁用状态。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="permissions"></a>Permissions  
 需要对指定的数据库拥有 ALTER DATABASE 权限。  
  
  
