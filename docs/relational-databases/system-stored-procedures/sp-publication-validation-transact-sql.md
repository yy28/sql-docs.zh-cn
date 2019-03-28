---
title: sp_publication_validation (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_publication_validation
- sp_publication_validation_TSQL
helpviewer_keywords:
- sp_publication_validation
ms.assetid: 06be2363-00c0-4936-97c1-7347f294a936
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 124d5d14f810a32e32ce92cbb96afe4569804c67
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58537169"
---
# <a name="sppublicationvalidation-transact-sql"></a>sp_publication_validation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为指定发布中的每个项目启动项目验证请求。 在发布服务器上对发布数据库执行此存储的过程。  
  
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
 [**@publication=**] **'**_publication'_  
 发布的名称。 *发布*是**sysname**，无默认值。  
  
 [**@rowcount_only=**] *rowcount_only*  
 指示是否只返回表的行计数。 *rowcount_only*是**smallint**可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**0**|执行与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 兼容的校验和。<br /><br /> 注意：水平筛选项目时，将执行行计数操作，而不是校验和操作。|  
|**1** （默认值）|仅执行行计数检查。|  
|**2**|执行行计数和二进制校验和。<br /><br /> 注意：对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 版订阅服务器，只执行行计数验证。|  
  
 [**@full_or_fast=**] *full_or_fast*  
 用于计算行计数的方法。 *full_or_fast*是**tinyint**可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**0**|使用 COUNT(*) 进行完整计数。|  
|**1**|快速从计数**sysindexes.rows**。 对行进行计数[sys.sysindexes](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md)比对实际表中的行计数要快得多。 但是，由于[sys.sysindexes](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md)是惰性更新，则 rowcount 可能不准确。|  
|**2** （默认值）|首先尝试使用快速方法进行条件性快速计数。 如果快速方法显示出差异，则转而使用完整方法。 如果*expected_rowcount*为 NULL，而且该存储的过程正在使用来获取此值，则始终使用完整 COUNT(*)。|  
  
`[ @shutdown_agent = ] shutdown_agent` 是分发代理是否应关闭立即验证完成后。 *shutdown_agent*是**位**，默认值为**0**。 如果**0**，复制代理不会关闭。 如果**1**，验证最后一篇文章后关闭复制代理。  
  
`[ @publisher = ] 'publisher'` 指定一个非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 *发布服务器*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  *发布服务器*上请求验证时不应使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_publication_validation**事务复制中使用。  
  
 **sp_publication_validation**可以在任何时间激活与该发布关联的文章后调用。 可以手动运行一次此过程，或将其作为验证数据的定期计划作业的一部分。  
  
 如果你的应用程序有即时更新订阅服务器， **sp_publication_validation**可能检测到假错误。 **sp_publication_validation**首先计算行计数或校验和，然后在发布服务器和订阅服务器。 由于在发布服务器中完成行计数或校验和之后，但在订阅服务器中完成行计数或校验和之前，即时更新触发器可以将更新从订阅服务器传播到发布服务器，因此值可能会更改。 若要确保在验证发布时，在订阅服务器和发布服务器中的值不发生更改，请在验证期间在发布服务器中停止 Microsoft 分布式事务处理协调器 (MS DTC) 服务。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_publication_validation**。  
  
## <a name="see-also"></a>请参阅  
 [验证订阅服务器上的数据](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [sp_article_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)   
 [sp_table_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-validation-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
