---
title: sp_dropserver (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_dropserver_TSQL
- sp_dropserver
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropserver
ms.assetid: 0fc83e35-0caa-49a3-a4b6-a1890d4f46ef
caps.latest.revision: 29
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 1aa8b62529bee6c5035161a9d7964c5f2f8ec5c7
ms.sourcegitcommit: d8e3da95f5a2b7d3997d63c53e722d494b878eec
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2018
ms.locfileid: "44171699"
---
# <a name="spdropserver-transact-sql"></a>sp_dropserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  从本地 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中的已知远程服务器和链接服务器的列表中删除服务器。  
  
 ![链接图标](../../database-engine/configure-windows/media/topic-link.gif "链接图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql  
sp_dropserver [ @server = ] 'server'   
     [ , [ @droplogins = ] { 'droplogins' | NULL} ]  
```  
  
## <a name="arguments"></a>参数  
 服务器  
 要删除的服务器。 *server* 的数据类型为 **sysname**，无默认值。 *服务器*必须存在。  
  
 *droplogins*  
 指示相关服务器远程和链接服务器登录名*服务器*如果还必须删除**droplogins**指定。 **`@droplogins`** 是**char （10)**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>Remarks  
 如果在运行**sp_dropserver**上具有关联的远程服务器和链接服务器登录名项或配置为复制发布服务器的服务器，则返回一条错误消息。 若要删除的服务器的所有远程服务器和链接服务器登录名时删除服务器，请使用**droplogins**参数。  
  
 **sp_dropserver**不能在用户定义的事务内执行。  
  
## <a name="permissions"></a>Permissions  
 要求对服务器拥有 ALTER ANY LINKED SERVER 权限。  
  
## <a name="examples"></a>示例  
 以下示例从本地 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例删除远程服务器 `ACCOUNTS` 以及所有关联的远程登录名。  
  
```  
sp_dropserver 'ACCOUNTS', 'droplogins';  
```  
  
## <a name="see-also"></a>请参阅  
 [安全存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addserver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_dropremotelogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropremotelogin-transact-sql.md)   
 [sp_helpremotelogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [sp_helpserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
