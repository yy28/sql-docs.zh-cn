---
title: sp_helplogins (Transact SQL) |Microsoft 文档
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
- sp_helplogins_TSQL
- sp_helplogins
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helplogins
ms.assetid: f9ad3767-5b9f-420d-8922-b637811404f7
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 40a25164c12e9a1c886a7cba6b8f9b0277daf0ed
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="sphelplogins-transact-sql"></a>sp_helplogins (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  提供有关每个数据库中的登录名以及与其相关的用户的信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helplogins [ [ @LoginNamePattern = ] 'login' ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@LoginNamePattern =** ] **'***login***'**  
 是登录名。 login 的数据类型为 sysname，默认值为 NULL。 *登录名*如果指定必须存在。 如果*登录*是未指定，则返回有关所有登录名的信息。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 第一个报告包含有关指定的每个登录的信息，如下表所示。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**LoginName**|**sysname**|登录名。|  
|**SID**|**varbinary(85)**|登录安全标识符 (SID)。|  
|**DefDBName**|**sysname**|默认数据库**LoginName**连接到的实例时使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|**DefLangName**|**sysname**|默认语言由**LoginName**。|  
|**某个用户**|**char(5)**|是 = **LoginName**数据库中有一个关联的用户名称。<br /><br /> 否 = **LoginName**没有关联的用户名。|  
|**远程**|**char(7)**|是 = **LoginName**具有关联的远程登录名。<br /><br /> 否 = **LoginName**没有关联的登录名。|  
  
 第二个报告包含有关映射到每个登录的用户的信息以及登录的角色成员身份，如下表所示。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**LoginName**|**sysname**|登录名。|  
|**DBName**|**sysname**|默认数据库**LoginName**连接到的实例时使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|**UserName**|**sysname**|用户帐户**LoginName**映射到在**DBName**，和角色， **LoginName**为在属于**DBName**。|  
|**UserOrAlias**|**char （8)**|MemberOf =**用户名**是一种角色。<br /><br /> 用户 =**用户名**是用户帐户。|  
  
## <a name="remarks"></a>注释  
 删除登录名之前, 使用**sp_helplogins**来标识映射到登录名的用户帐户。  
  
## <a name="permissions"></a>权限  
 要求的成员身份**securityadmin**固定的服务器角色。  
  
 若要标识所有用户帐户映射到给定的登录名， **sp_helplogins**必须检查服务器内的所有数据库。 因此，对于服务器中的每个数据库，至少应满足下列条件之一：  
  
-   正在执行的用户**sp_helplogins**有权访问数据库。  
  
-   **来宾**在数据库中启用用户帐户。  
  
 如果**sp_helplogins**无法访问数据库， **sp_helplogins**将返回尽可能多的信息，因为它会显示错误消息 15622。  
  
## <a name="examples"></a>示例  
 以下示例报告有关登录 `John` 的信息。  
  
```  
EXEC sp_helplogins 'John';  
GO  
  
LoginName SID                        DefDBName DefLangName AUser ARemote   
--------- -------------------------- --------- ----------- ----- -------   
John      0x23B348613497D11190C100C  master    us_english  yes   no  
  
(1 row(s) affected)  
  
LoginName   DBName   UserName   UserOrAlias   
---------   ------   --------   -----------   
John        pubs     John       User          
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另请参阅  
 [安全存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_helpdb &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)   
 [sp_helpuser &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
