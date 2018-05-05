---
title: sp_article_validation (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/16/2017
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
- sp_article_validation_TSQL
- sp_article_validation
helpviewer_keywords:
- sp_article_validation
ms.assetid: 44e7abcd-778c-4728-a03e-7e7e78d3ce22
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 8eabbaf95392de7e5389fdd54f8724045682ec2a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sparticlevalidation-transact-sql"></a>sp_article_validation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为指定项目启动数据验证请求。 此存储过程在发布服务器上的发布数据库中执行，或者在订阅服务器上的订阅数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_article_validation [ @publication = ] 'publication'  
    [ , [ @article = ] 'article' ]  
    [ , [ @rowcount_only = ] type_of_check_requested ]  
    [ , [ @full_or_fast = ] full_or_fast ]  
    [ , [ @shutdown_agent = ] shutdown_agent ]  
    [ , [ @subscription_level = ] subscription_level ]  
    [ , [ @reserved = ] reserved ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@publication=**] **'***publication***'**  
 包含该项目的发布的名称。 *发布*是**sysname**，无默认值。  
  
 [  **@article=**] *****文章*****  
 要验证的项目的名称。 *文章*是**sysname**，无默认值。  
  
 [  **@rowcount_only=**] *type_of_check_requested*  
 指定是否只返回表的行计数。 *type_of_check_requested*是**smallint**，默认值为**1**。  
  
 如果**0**，执行行计数和[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 兼容的校验和。  
  
 如果**1**，执行行计数检查。  
  
 如果**2**，执行行计数和二进制校验和。  
  
 [  **@full_or_fast=**] *full_or_fast*  
 用于计算行计数的方法。 *full_or_fast*是**tinyint**，并且可以为这些值之一。  
  
|**Value**|**Description**|  
|---------------|---------------------|  
|**0**|用 COUNT(*) 执行完整计数。|  
|**1**|执行中的快速计数**sysindexes.rows**。 计算行数**sysindexes**快于计算实际的表中的行数。 但是， **sysindexes**延迟，更新和行计数可能不准确。|  
|**2** （默认值）|首先尝试使用快速方法执行条件性快速计数。 如果快速方法显示出差异，则转而使用完整方法。 如果*expected_rowcount*为 NULL，而存储的过程正在使用来获取的值，始终使用完整 COUNT(*)。|  
  
 [  **@shutdown_agent=**] *shutdown_agent*  
 指定分发代理是否应在完成验证后立即关闭。 *shutdown_agent*是**位**，默认值为**0**。 如果**0**，分发代理不会关闭。 如果**1**，验证项目之后，分发代理关闭。  
  
 [  **@subscription_level=**] *subscription_level*  
 指定是否由订阅服务器集来拾取验证。 *subscription_level*是**位**，默认值为**0**。 如果**0**，验证应用到所有订阅服务器。 如果**1**，验证仅适用于通过调用指定的订阅服务器的子集**sp_marksubscriptionvalidation**中当前打开的事务。  
  
 [  **@reserved=**]*保留*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [ **@publisher**=] *****发布服务器*****  
 指定一个非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 *发布服务器*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  *发布服务器*上请求验证时不应使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_article_validation**事务复制中使用。  
  
 **sp_article_validation**导致收集到指定的项目不验证信息并发布到事务日志的验证请求。 分发代理接收到该请求后，将该请求中的验证信息与订阅服务器表进行比较。 验证的结果显示在复制监视器和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理警报中。  
  
## <a name="permissions"></a>权限  
 仅具有的用户选择的可以执行所验证的文章在源表上的所有权限**sp_article_validation**。  
  
## <a name="see-also"></a>另请参阅  
 [验证复制的数据](../../relational-databases/replication/validate-replicated-data.md)   
 [sp_marksubscriptionvalidation &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-marksubscriptionvalidation-transact-sql.md)   
 [sp_publication_validation &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)   
 [sp_table_validation &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-validation-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
