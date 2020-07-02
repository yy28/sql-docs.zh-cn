---
title: sp_db_increased_partitions |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_db_increased_partitions_TSQL
- sp_db_increased_partitions
dev_langs:
- TSQL
helpviewer_keywords:
- sp_db_increased_partitions
ms.assetid: a8c043ec-b504-4929-ac0e-8babaa99d989
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b93680fd4a4688aa36243f0d09c491254e9aa378
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85760164"
---
# <a name="sp_db_increased_partitions"></a>sp_db_increased_partitions
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  对指定的数据库启用或禁用对多达 15000 个分区的支持。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_dp_increased_partitions   
[ @dbname ] = 'database_name'   
[ , [ @increased_partitions = ] 'increased_partitions' ] [;]  
```  
  
## <a name="arguments"></a>自变量  
 [ @dbname =] "*database_name*"  
 数据库的名称。 在**sysname** *中，默认*值为 NULL。 如果未指定*dbname* ，则使用当前数据库。  
  
 [ @increased_partitions =] "*increased_partitions*"  
 对指定的数据库启用或禁用对 15000 个分区的支持。 *increased_partitions*的值为**varchar （6）** ，默认值为 NULL。 要启用支持，则接受的值是“ON”或“TRUE”；要禁用支持，则接受的值为“OFF”和“FALSE”。 如果未指定*increased_partitions* ，则该过程将返回1，表示已对指定的数据库启用支持，或为0以指示禁用了支持。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="permissions"></a>权限  
 需要对指定的数据库拥有 ALTER DATABASE 权限。  
  
  
