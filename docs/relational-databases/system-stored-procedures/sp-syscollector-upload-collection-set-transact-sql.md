---
title: sp_syscollector_upload_collection_set (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_upload_collection_set
- sp_syscollector_upload_collection_set_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_upload_collection_set
- data collector [SQL Server], stored procedures
ms.assetid: eed9232c-2b0a-4b6a-8ba0-76b7c99f48dc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d246e2817c34449ab6d4dd5d3def62feba92b196
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63001308"
---
# <a name="spsyscollectoruploadcollectionset-transact-sql"></a>sp_syscollector_upload_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在启用了收集组时启动收集组数据的上载。  
  
> [!IMPORTANT]  
>  此存储过程只能用于配置为缓存模式的数据收集和上载的收集组。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_syscollector_upload_collection_set [[ @collection_set_id = ] collection_set_id ]  
          , [[ @name = ] 'name' ]   
```  
  
## <a name="arguments"></a>参数  
`[ @collection_set_id = ] collection_set_id` 是收集组的唯一本地标识符。 *collection_set_id*是**int**并且必须具有一个值，如果*名称*为 NULL。  
  
`[ @name = ] 'name'` 是收集组的名称。 *名称*是**sysname**并且必须具有一个值，如果*collection_set_id*为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 任一*collection_set_id*或*名称*必须具有值; 都不能为 NULL。  
  
 此过程可用于为正在运行的收集组启动按需上载。 它只能用于配置为缓存模式的数据收集和上载的收集组。 这使用户能够获取数据以进行分析而不必等待所计划的上载过程。  
  
## <a name="permissions"></a>权限  
 要求的成员身份**dc_operator** （拥有 EXECUTE 权限） 固定的数据库角色来执行此过程。  
  
## <a name="example"></a>示例  
 执行一个名为 `Simple Collection Set` 的收集组的按需上载。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_upload_collection_set @name = 'Simple Collection Set' ;  
```  
  
## <a name="see-also"></a>请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [“数据收集”](../../relational-databases/data-collection/data-collection.md)  
  
  
