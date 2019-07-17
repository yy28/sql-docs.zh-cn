---
title: sp_helparticledts (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helparticledts
- sp_helparticledts_TSQL
helpviewer_keywords:
- sp_helparticledts
ms.assetid: cd1aed60-e056-4ff3-86ee-62b19433d890
author: stevestein
ms.author: sstein
ms.openlocfilehash: 153b7736f126a09765eaac4c364b322fffc96c48
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68084948"
---
# <a name="sphelparticledts-transact-sql"></a>sp_helparticledts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  用于获取使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 创建事务订阅时所用的正确自定义任务名称的信息。 在发布服务器上对发布数据库执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helparticledts [ @publication = ] 'publication', [ @article = ] 'article'  
```  
  
## <a name="arguments"></a>参数  
`[ @publication = ] 'publication'` 是发布的名称。 *发布*是**sysname**，无默认值。  
  
`[ @article = ] 'article'` 是发布中的名称。 *文章*是**sysname**，无默认值。  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**pre_script_ignore_error_task_name**|**sysname**|在复制快照数据之前发生的编程任务的名称。 如果遇到脚本错误，程序应继续执行。|  
|**pre_script_task_name**|**sysname**|在复制快照数据之前发生的编程任务的名称。 遇到错误时程序将停止执行。|  
|**transformation_task_name**|**sysname**|使用数据驱动的查询任务时的编程任务的名称。|  
|**post_script_ignore_error_task_name**|**sysname**|复制快照数据之后发生的编程任务的名称。 如果遇到脚本错误，程序应继续执行。|  
|**post_script_task_name**|**sysname**|复制快照数据之后发生的编程任务的名称。 遇到错误时程序将停止执行。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_helparticledts**快照复制和事务复制中使用。  
  
 在复制 Data Transformation Services (DTS) 程序中命名任务时，必须遵从复制代理所需的某些命名约定。 对于自定义任务（如执行 SQL 任务），名称是由项目名称、前缀和可选部分组成的串联字符串。 编写代码时，如果不能确定任务名，则结果集将给出应使用的任务名。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色和**db_owner**固定的数据库角色可以执行**sp_helparticledts**。  
  
  
