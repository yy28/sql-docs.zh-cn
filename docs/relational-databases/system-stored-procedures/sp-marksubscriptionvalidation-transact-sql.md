---
title: sp_marksubscriptionvalidation (Transact SQL) |Microsoft 文档
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
- sp_marksubscriptionvalidation
- sp_marksubscriptionvalidation_TSQL
helpviewer_keywords:
- sp_marksubscriptionvalidation
ms.assetid: e68fe0b9-5993-4880-917a-b0f661f8459b
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 1b088b43cfc625591d5160b6818949b0c933a696
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32997684"
---
# <a name="spmarksubscriptionvalidation-transact-sql"></a>sp_marksubscriptionvalidation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  将当前打开的事务，要指定的订阅服务器的订阅级别验证事务的标记。 在发布服务器的发布数据库上执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_marksubscriptionvalidation [ @publication = ] 'publication'  
        , [ @subscriber = ] 'subscriber'  
        , [ @destination_db = ] 'destination_db'  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@publication**=] *****发布*****  
 发布的名称。 *发布*是**sysname**，无默认值。  
  
 [ **@subscriber**=] *****订阅服务器*****  
 订阅服务器的名称。 *订阅服务器*为 sysname，无默认值。  
  
 [  **@destination_db=**] *****destination_db*****  
 目标数据库的名称。 *destination_db*是**sysname**，无默认值。  
  
 [  **@publisher=** ] *****发布服务器*****  
 指定一个非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 *发布服务器*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  *发布服务器*不应该用于所属的发布[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_marksubscriptionvalidation**事务复制中使用。  
  
 **sp_marksubscriptionvalidation**不支持非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]订阅服务器。  
  
 有关非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器，则无法执行**sp_marksubscriptionvalidation**从在显式事务中。 这是因为在用于访问发布服务器的链接服务器连接上，不支持显式事务。  
  
 **sp_marksubscriptionvalidation**必须连同使用[sp_article_validation &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)，将值指定为**1**为*subscription_level*，并可与其他调用使用**sp_marksubscriptionvalidation**将标记为其他订阅服务器当前打开的事务。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_marksubscriptionvalidation**。  
  
## <a name="example"></a>示例  
 下面的查询可应用到发布数据库，以发布订阅级验证命令。 下列命令将由指定的订阅服务器的分发代理程序挑选。 请注意第一个事务验证文章**art1**'，而第二事务验证'**art2**。 另请注意，对的调用**sp_marksubscriptionvalidation**和[sp_article_validation &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)已封装在事务中。 我们建议仅一次调用[sp_article_validation &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)每个事务。 这是因为[sp_article_validation &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)事务的持续时间在源表上包含共享的表锁。 应尽量缩短事务以使并发最大化。  
  
```  
begin tran  
  
exec sp_marksubscriptionvalidation @publication = 'pub1',  
 @subscriber = 'Sub', @destination_db = 'SubDB'  
  
exec sp_marksubscriptionvalidation @publication = 'pub1',  
 @subscriber = 'Sub2', @destination_db = 'SubDB'  
  
exec sp_article_validation @publication = 'pub1', @article = 'art1',  
 @rowcount_only = 0, @full_or_fast = 0, @shutdown_agent = 0,  
 @subscription_level = 1  
  
commit tran  
  
begin tran  
  
exec sp_marksubscriptionvalidation @publication = 'pub1',  
 @subscriber = 'Sub', @destination_db = 'SubDB'  
  
exec sp_marksubscriptionvalidation @publication = 'pub1',  
 @subscriber = 'Sub2', @destination_db = 'SubDB'  
  
exec sp_article_validation @publication = 'pub1', @article = 'art2',  
 @rowcount_only = 0, @full_or_fast = 0, @shutdown_agent = 0,  
 @subscription_level = 1  
  
commit tran  
```  
  
## <a name="see-also"></a>另请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [验证已复制的数据](../../relational-databases/replication/validate-replicated-data.md)  
  
  
