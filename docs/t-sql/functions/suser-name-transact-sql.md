---
title: "SUSER_NAME (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SUSER_NAME
- SUSER_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- security identification names [SQL Server]
- logins [SQL Server], users
- identification names for logins [SQL Server]
- users [SQL Server], logins
- SUSER_NAME function
- logins [SQL Server], names
- names [SQL Server], logins
ms.assetid: ae598d9f-9baa-49b8-b1c1-042854206de4
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a8d4eae9424d5c5cb2dbb2e7851d4e660fa0ba72
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="susername-transact-sql"></a>SUSER_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  返回用户的登录标识名。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
SUSER_NAME ( [ server_user_id ] )   
```  
  
## <a name="arguments"></a>参数  
 *server_user_id*  
 用户的登录标识号。 *server_user_id*，这是可选的是**int**。*server_user_id*可以是任意的登录标识号[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名或[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows 用户或组有权连接到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果*server_user_id*是未指定，则返回当前用户的登录名标识名称。 如果此参数包含词 NULL，将返回 NULL。  
  
## <a name="return-types"></a>返回类型  
 **nvarchar （128)**  
  
## <a name="remarks"></a>注释  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 中，安全标识号 (SID) 取代了服务器用户标识号 (SUID)。  
  
 SUSER_NAME 返回仅有一个条目中的登录名的登录名**syslogins**系统表。  
  
 SUSER_NAME 可以在选择列表、WHERE 子句和任何允许使用表达式的地方使用，并且后面必须始终要有一对圆括号，即使未指定任何参数时也是如此。  
  
## <a name="examples"></a>示例  
 以下示例将返回登录标识号为 `1` 的用户的登录标识名。  
  
```  
SELECT SUSER_NAME(1);  
```  
  
## <a name="see-also"></a>另请参阅  
 [SUSER_ID &#40;Transact SQL &#41;](../../t-sql/functions/suser-id-transact-sql.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
