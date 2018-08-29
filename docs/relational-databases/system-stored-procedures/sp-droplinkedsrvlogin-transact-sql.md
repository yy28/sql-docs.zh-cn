---
title: sp_droplinkedsrvlogin (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_droplinkedsrvlogin_TSQL
- sp_droplinkedsrvlogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_droplinkedsrvlogin
ms.assetid: 75a4a040-72d5-4d29-8304-de0aa481ad4b
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6e85ed0511ea1986bc19f46903513dfd8a5bc2c1
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43021008"
---
# <a name="spdroplinkedsrvlogin-transact-sql"></a>sp_droplinkedsrvlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本地服务器上的登录与链接服务器上的登录之间的现有映射。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_droplinkedsrvlogin [ @rmtsrvname= ] 'rmtsrvname' ,   
   [ @locallogin= ] 'locallogin'  
```  
  
## <a name="arguments"></a>参数  
 [  **@rmtsrvname =** ] **'***rmtsrvname*****  
 链接服务器的名称，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]应用登录映射。 *rmtsrvname*是**sysname**，无默认值。 *rmtsrvname*必须已经存在。  
  
 [  **@locallogin =** ] **'***locallogin*****  
 是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]映射到链接服务器的本地服务器上的登录名*rmtsrvname*。 *locallogin*是**sysname**，无默认值。 映射*locallogin*到*rmtsrvname*必须已经存在。 如果为 NULL，默认映射创建的**sp_addlinkedserver**，这将在本地服务器上的所有登录名映射到链接服务器上的登录名被删除。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>Remarks  
 本地服务器的现有映射删除登录名，当使用创建的默认映射**sp_addlinkedserver**当它连接到链接服务器代表该登录名。 若要更改默认映射，请使用**sp_addlinkedsrvlogin**。  
  
 如果默认映射也被删除，只有已显式授予登录名映射到链接服务器的使用的登录名**sp_addlinkedsrvlogin**，可以访问链接的服务器。  
  
 **sp_droplinkedsrvlogin**不能从用户定义的事务内执行。  
  
## <a name="permissions"></a>Permissions  
 要求对服务器拥有 ALTER ANY LOGIN 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-removing-the-login-mapping-for-an-existing-user"></a>A. 为现有用户删除登录映射  
 以下示例删除从本地服务器到链接服务器 `Mary` 的登录 `Accounts` 的映射。 因此，登录 `Mary` 使用默认登录映射。  
  
```  
EXEC sp_droplinkedsrvlogin 'Accounts', 'Mary';  
```  
  
### <a name="b-removing-the-default-login-mapping"></a>B. 删除默认的登录映射  
 以下示例删除最初通过在链接服务器 `sp_addlinkedserver` 上执行 `Accounts` 而创建的默认登录映射。  
  
```  
EXEC sp_droplinkedsrvlogin 'Accounts', NULL;  
```  
  
## <a name="see-also"></a>请参阅  
 [sp_addlinkedserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
