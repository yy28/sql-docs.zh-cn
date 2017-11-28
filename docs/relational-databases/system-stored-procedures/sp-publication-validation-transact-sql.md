---
title: "sp_publication_validation (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_publication_validation
- sp_publication_validation_TSQL
helpviewer_keywords: sp_publication_validation
ms.assetid: 06be2363-00c0-4936-97c1-7347f294a936
caps.latest.revision: "34"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c08dc184475526abd962ab97f52ccfbb8c405e8f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="sppublicationvalidation-transact-sql"></a>sp_publication_validation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为指定发布中的每个项目启动项目验证请求。 在发布服务器的发布数据库上执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_publication_validation [ @publication = ] 'publication'  
    [ , [ @rowcount_only = ] type_of_check_requested ]  
    [ , [ @full_or_fast = ] full_or_fast ]  
    [ , [ @shutdown_agent = ] shutdown_agent ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>参数  
 [**@publication=**] *发布*  
 发布的名称。 *发布*是**sysname**，无默认值。  
  
 [**@rowcount_only=**] *rowcount_only*  
 指示是否只返回表的行计数。 *rowcount_only*是**smallint**和可以是以下值之一。  
  
|值|说明|  
|-----------|-----------------|  
|**0**|执行与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 兼容的校验和。<br /><br /> 注意： 当项目进行水平筛选时，将而不是校验和操作执行行计数操作。|  
|**1** （默认值）|仅执行行计数检查。|  
|**2**|执行行计数和二进制校验和。<br /><br /> 注意： 对于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]执行版本 7.0 订阅服务器，仅行计数验证。|  
  
 [**@full_or_fast=**] *full_or_fast*  
 用于计算行计数的方法。 *full_or_fast*是**tinyint**和可以是以下值之一。  
  
|值|说明|  
|-----------|-----------------|  
|**0**|使用 COUNT(*) 进行完整计数。|  
|**1**|未快速从计数**sysindexes.rows**。 计算行数[sys.sysindexes](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md)比计算实际的表中的行数快得多。 但是，因为[sys.sysindexes](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md)是延迟更新，则行计数可能不准确。|  
|**2** （默认值）|首先尝试使用快速方法进行条件性快速计数。 如果快速方法显示出差异，则转而使用完整方法。 如果*expected_rowcount*为 NULL，而存储的过程正在使用来获取的值，始终使用完整 COUNT(*)。|  
  
 [  **@shutdown_agent=**] *shutdown_agent*  
 指示分发代理是否应在完成验证后立即关闭。 *shutdown_agent*是**位**，默认值为**0**。 如果**0**，复制代理不会关闭。 如果**1**，验证最后一篇文章之后，复制代理关闭。  
  
 [  **@publisher**  =] *发布服务器*  
 指定非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布服务器。 *发布服务器*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  *发布服务器*上请求验证时不应使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_publication_validation**事务复制中使用。  
  
 **sp_publication_validation**可以在后已激活与发布关联的文章的任意时间调用。 可以手动运行一次此过程，或将其作为验证数据的定期计划作业的一部分。  
  
 如果应用程序的立即更新订阅服务器， **sp_publication_validation**可能会检测到虚假错误。 **sp_publication_validation**首先计算的行计数或校验和发布服务器上，然后在订阅服务器上。 由于在发布服务器中完成行计数或校验和之后，但在订阅服务器中完成行计数或校验和之前，即时更新触发器可以将更新从订阅服务器传播到发布服务器，因此值可能会更改。 若要确保在验证发布时，在订阅服务器和发布服务器中的值不发生更改，请在验证期间在发布服务器中停止 Microsoft 分布式事务处理协调器 (MS DTC) 服务。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_publication_validation**。  
  
## <a name="see-also"></a>另请参阅  
 [验证订阅服务器上的数据](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [sp_article_validation &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)   
 [sp_table_validation &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-table-validation-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
