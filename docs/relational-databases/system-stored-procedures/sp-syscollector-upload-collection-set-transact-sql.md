---
title: sp_syscollector_upload_collection_set （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9302728bf93a53ce333dce5a38bfa7e046d38fe0
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82824234"
---
# <a name="sp_syscollector_upload_collection_set-transact-sql"></a>sp_syscollector_upload_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在启用了收集组时启动收集组数据的上载。  
  
> [!IMPORTANT]  
>  此存储过程只能用于配置为缓存模式的数据收集和上载的收集组。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_syscollector_upload_collection_set [[ @collection_set_id = ] collection_set_id ]  
          , [[ @name = ] 'name' ]   
```  
  
## <a name="arguments"></a>参数  
`[ @collection_set_id = ] collection_set_id`收集组的唯一本地标识符。 *collection_set_id*为**int** ，并且*name*为 NULL 时必须具有值。  
  
`[ @name = ] 'name'`收集组的名称。 *名称*为**sysname** ，并且*collection_set_id*为 NULL 时必须具有值。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="remarks"></a>备注  
 *Collection_set_id*或*name*必须具有值;两者都不能为 NULL。  
  
 此过程可用于为正在运行的收集组启动按需上载。 它只能用于配置为缓存模式的数据收集和上载的收集组。 这使用户能够获取数据以进行分析而不必等待所计划的上载过程。  
  
## <a name="permissions"></a>权限  
 需要**dc_operator** （具有 execute 权限）的成员身份才能执行此过程。  
  
## <a name="example"></a>示例  
 执行一个名为 `Simple Collection Set` 的收集组的按需上载。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_upload_collection_set @name = 'Simple Collection Set' ;  
```  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Transact-sql&#41;系统存储过程](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [数据收集](../../relational-databases/data-collection/data-collection.md)  
  
  
