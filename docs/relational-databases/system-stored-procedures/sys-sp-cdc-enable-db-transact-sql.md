---
title: sys.sp_cdc_enable_db (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cdc_enable_db_TSQL
- sp_cdc_enable_db
- sys.sp_cdc_enable_db
- sys.sp_cdc_enable_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_cdc_enable_db
- change data capture [SQL Server], enabling databases
- sp_cdc_enable_db
ms.assetid: 176d83b3-493d-43cd-800e-aa123c3bdf17
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0f8c68e5366d8cd55475621ff4985c48a47ed4ae
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43030281"
---
# <a name="sysspcdcenabledb-transact-sql"></a>sys.sp_cdc_enable_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  对当前数据库启用变更数据捕获。 必须先对数据库执行此过程，然后才能对该数据库中的任何表启用变更数据捕获。 变更数据捕获可记录应用到所启用的表中的插入、更新和删除活动，同时采用易于使用的关系格式提供变更详细信息。 此操作将为已修改的行捕获反映了所跟踪源表列结构的列信息，同时还捕获将更改应用到目标环境所需的元数据。  
  
> [!IMPORTANT]  
>  并非在 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的每个版本中均提供变更数据捕获功能。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]各版本支持的功能列表，请参阅 [SQL Server 2016 各个版本支持的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.sp_cdc_enable_db  
```  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="remarks"></a>Remarks  
 无法上启用变更数据捕获[系统数据库](../../relational-databases/databases/system-databases.md)或分发数据库。  
  
 sys.sp_cdc_enable_db 将创建以全数据库为作用域的变更数据捕获对象，包括元数据表和 DDL 触发器。 它还会创建 cdc 架构和 cdc 数据库用户并设置中的数据库条目的 is_cdc_enabled 列[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)目录视图为 1。  
  
## <a name="permissions"></a>Permissions  
 要求具有 sysadmin 固定服务器角色的成员身份。  
  
## <a name="examples"></a>示例  
 下面的示例启用了变更数据捕获。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_enable_db;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [sys.sp_cdc_disable_db &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md)  
  
  
