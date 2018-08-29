---
title: sp_help_publication_access (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sp_help_publication_access
- sp_help_publication_access_TSQL
helpviewer_keywords:
- sp_help_publication_access
ms.assetid: 9408fa13-54a0-4cb1-8fb0-845e5536ef50
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 803b5d26fa2294a9e53d3afb597a232384dfd38d
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43036182"
---
# <a name="sphelppublicationaccess-transact-sql"></a>sp_help_publication_access (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回发布的所有授权登录的列表。 在发布服务器上对发布数据库执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_help_publication_access [ @publication = ] 'publication'  
    [ , [ @return_granted = ] 'return_granted' ]   
    [ , [ @login = ] 'login' ]  
    [ , [ @initial_list = ] initial_list ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@publication=**] **'***publication***'**  
 要访问的发布名称。 *发布*是**sysname**，无默认值。  
  
 [  **@return_granted=**] **'***return_granted*****  
 登录名 ID。 *return_granted*是**位**，默认值为 1。 如果**0**指定和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用身份验证，返回出现在发布服务器而不是在分发服务器上的可用登录。 如果**0**指定和使用 Windows 身份验证、 登录名没有被明确拒绝访问在发布服务器或分发服务器返回。  
  
 [  **@login=**] **'***登录*****  
 标准安全登录 ID。 *登录名*是**sysname**，默认值为**%**。  
  
 [  **@initial_list =**] *initial_list*  
 指定是返回具有发布访问权的所有成员，还是只返回那些在新成员添加到列表之前具有访问权的成员。 *initial_list*为 bit，默认值为**0**。  
  
 **1**返回的所有成员的信息**sysadmin**与已存在时创建发布，分发服务器上的有效登录名，以及当前登录名的固定的服务器角色。  
  
 **0**返回的所有成员的信息**sysadmin**固定的服务器角色并具有有效登录名，在分发服务器时创建发布还为所有用户发布访问列表中存在已不这样做属于**sysadmin**固定的服务器角色。  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**Loginname**|**nvarchar(256)**|实际登录名。|  
|**isntname**|**int**|**0** = 登录名不是 Windows 用户。<br /><br /> **1** = 登录名是 Windows 用户。|  
|**isntgroup**|**int**|**0** = 登录名不是 Windows 组。<br /><br /> **1** = 登录名是 Windows 组。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>Remarks  
 **sp_help_publication_access**用于所有类型的复制。  
  
 时同时**Isntname**和**Isntgroup**在结果集是**0**，则假定该登录名是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_help_publication_access**。  
  
## <a name="see-also"></a>请参阅  
 [sp_grant_publication_access &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-publication-access-transact-sql.md)   
 [sp_revoke_publication_access &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-publication-access-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
