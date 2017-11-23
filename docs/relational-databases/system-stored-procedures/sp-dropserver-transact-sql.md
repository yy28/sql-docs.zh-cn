---
title: "sp_dropserver (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_dropserver_TSQL
- sp_dropserver
dev_langs: TSQL
helpviewer_keywords: sp_dropserver
ms.assetid: 0fc83e35-0caa-49a3-a4b6-a1890d4f46ef
caps.latest.revision: "29"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 256bb358f11443824e2d4aae4a2a3b4bed31b00e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spdropserver-transact-sql"></a>sp_dropserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从本地 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中的已知远程服务器和链接服务器的列表中删除服务器。  
  
||  
|-|  
|**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。|  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_dropserver [ @server = ] 'server'   
     [ , [ @droplogins = ] { 'droplogins' | NULL} ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@server =** ] *服务器*  
 要删除的服务器。 *server* 的数据类型为 **sysname**，无默认值。 *服务器*必须存在。  
  
 [  **@droplogins =** ] **droplogins** |NULL  
 指示相关的远程和链接服务器登录名*服务器*如果还必须删除**droplogins**指定。 **@droplogins**是**char （10)**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>注释  
 如果你运行**sp_dropserver**在服务器上具有关联的远程和链接服务器登录名条目，或配置为复制发布服务器，会返回错误消息。 若要删除服务器时，请删除所有服务器的远程和链接服务器登录名，使用**droplogins**自变量。  
  
 **sp_dropserver**不能在用户定义的事务内执行。  
  
## <a name="permissions"></a>Permissions  
 要求对服务器拥有 ALTER ANY LINKED SERVER 权限。  
  
## <a name="examples"></a>示例  
 以下示例从本地 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例删除远程服务器 `ACCOUNTS` 以及所有关联的远程登录名。  
  
```  
sp_dropserver 'ACCOUNTS', 'droplogins';  
```  
  
## <a name="see-also"></a>另请参阅  
 [安全存储过程 &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addserver &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_dropremotelogin &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropremotelogin-transact-sql.md)   
 [sp_helpremotelogin &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [sp_helpserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
