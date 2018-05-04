---
title: sp_syscollector_run_collection_set (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
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
- sp_syscollector_run_collection_set_TSQL
- sp_syscollector_run_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_run_collection_set
- data collector [SQL Server], stored procedures
ms.assetid: 7bbaee48-dfc7-45c0-b11f-c636b6a7e720
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b933787dabda07557bf798ef45d0611938f42a41
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spsyscollectorruncollectionset-transact-sql"></a>sp_syscollector_run_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  如果已启用收集器并将收集组配置为非缓存收集模式，则启动收集组。  
  
> [!NOTE]  
>  如果针对配置为缓存收集模式的收集组运行此过程，则会失败。  
  
 利用 sp_syscollector_run_collection_set，用户能够根据需要创建数据快照。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_syscollector_run_collection_set [[ @collection_set_id = ] collection_set_id ]  
          , [[ @name = ] 'name' ]   
```  
  
## <a name="arguments"></a>参数  
 [ **@collection_set_id =** ] *collection_set_id*  
 收集组的唯一本地标识符。 *collection_set_id*是**int**并且必须具有一个值，如果*名称*为 NULL。  
  
 [ **@name =** ] **'***name***'**  
 是的收集组的名称。 *名称*是**sysname**并且必须具有一个值，如果*collection_set_id*为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 任一*collection_set_id*或*名称*必须具有一个值，都不能为 NULL。  
  
 此过程将开始收集，并为指定的集合设置，并将立即启动集合代理作业，如果收集组已上载作业其**@collection_mode**设置为非缓存 (1)。 有关详细信息，请参阅[sp_syscollector_create_collection_set &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)。  
  
 sp_sycollector_run_collection_set 还可用于运行没有计划的收集组。  
  
## <a name="permissions"></a>权限  
 要求的成员身份**dc_operator** （拥有 EXECUTE 权限） 固定的数据库角色来执行此过程。  
  
## <a name="example"></a>示例  
 使用收集组的标识符启动收集组。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_run_collection_set @collection_set_id = 1;  
```  
  
## <a name="see-also"></a>另请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [数据收集](../../relational-databases/data-collection/data-collection.md)  
  
  
