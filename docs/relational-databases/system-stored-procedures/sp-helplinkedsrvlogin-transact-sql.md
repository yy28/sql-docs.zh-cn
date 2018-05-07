---
title: sp_helplinkedsrvlogin (Transact SQL) |Microsoft 文档
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
- sp_helplinkedsrvlogin_TSQL
- sp_helplinkedsrvlogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helplinkedsrvlogin
ms.assetid: a2b1eba0-bf71-47e7-a4c7-9f55feec82a3
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: b9615c833939c18b3653fa4035258b91bb5bdfc8
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="sphelplinkedsrvlogin-transact-sql"></a>sp_helplinkedsrvlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  提供有关某些登录名映射的信息，这些登录名是针对特定的链接服务器定义的，而这些链接服务器是用于分布式查询和远程存储过程的。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helplinkedsrvlogin [ [ @rmtsrvname = ] 'rmtsrvname' ]   
     [ , [ @locallogin = ] 'locallogin' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@rmtsrvname=**] *****rmtsrvname*****  
 登录映射所应用于的链接服务器的名称。 *rmtsrvname*是**sysname**，默认值为 NULL。 如果为 NULL，则返回针对所有链接服务器定义的所有登录映射，这些链接服务器在运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本地计算机中定义。  
  
 [  **@locallogin=**] *****locallogin*****  
 是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]具有到链接服务器的映射的本地服务器上的登录名*rmtsrvname*。 *locallogin*是**sysname**，默认值为 NULL。 NULL 指定所有登录名映射定义上*rmtsrvname*返回。 如果不是 NULL 的映射*locallogin*到*rmtsrvname*必须已存在。 *locallogin*可以是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名或 Windows 用户。 对于 Windows 用户来说，必须以直接的方式或通过已被授权访问的 Windows 组成员身份授予其访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的权限。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**链接的服务器**|**sysname**|链接服务器名称。|  
|**本地登录名**|**sysname**|本地登录，映射应用于该本地登录。|  
|**自助映射**|**int**|0 =**本地登录**映射到**远程登录**时连接到**链接服务器**。<br /><br /> 1 =**本地登录**映射到相同的登录名和密码连接到时**链接服务器**。|  
|**远程登录**|**sysname**|上的登录名**LinkedServer**映射到**LocalLogin**时**IsSelfMapping**为 0。 如果**IsSelfMapping**为 1， **RemoteLogin**为 NULL。|  
  
## <a name="remarks"></a>注释  
 删除登录名映射之前，请使用**sp_helplinkedsrvlogin**以确定所涉及的链接的服务器。  
  
## <a name="permissions"></a>权限  
 将不检查任何权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-displaying-all-login-mappings-for-all-linked-servers"></a>A. 显示所有链接服务器的所有登录映射  
 以下示例显示所有链接服务器的所有登录映射，这些链接服务器在运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本地计算机上定义。  
  
```  
EXEC sp_helplinkedsrvlogin;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Linked Server    Local Login   Is Self Mapping Remote Login   
---------------- ------------- --------------- --------------   
Accounts         NULL          1               NULL  
Sales            NULL          1               NULL  
Sales            Mary          0               sa  
Marketing        NULL          1               NULL  
  
(4 row(s) affected)  
```  
  
### <a name="b-displaying-all-login-mappings-for-a-linked-server"></a>B. 显示某个链接服务器的所有登录映射  
 以下示例显示 `Sales` 链接服务器的所有本地定义的登录映射。  
  
```  
EXEC sp_helplinkedsrvlogin 'Sales';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Linked Server    Local Login   Is Self Mapping Remote Login   
---------------- ------------- --------------- --------------   
Sales            NULL          1               NULL  
Sales            Mary          0               sa  
  
(2 row(s) affected)  
```  
  
### <a name="c-displaying-all-login-mappings-for-a-local-login"></a>C. 显示某个本地登录的所有登录映射  
 以下示例显示登录 `Mary` 的所有在本地定义的登录映射。  
  
```  
EXEC sp_helplinkedsrvlogin NULL, 'Mary';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Linked Server    Local Login   Is Self Mapping Remote Login   
---------------- ------------- --------------- --------------   
Sales            NULL          1               NULL  
Sales            Mary          0               sa  
  
(2 row(s) affected)  
```  
  
## <a name="see-also"></a>另请参阅  
 [安全存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addlinkedserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_droplinkedsrvlogin &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
