---
title: sp_changedistributor_password (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_changedistributor_password
- sp_changedistributor_password_TSQL
helpviewer_keywords:
- sp_changedistributor_password
ms.assetid: 4a496e60-414a-4026-ba7a-3e89391d39b7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e64397d7282960b580beda8cbe52c4c7092844b7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47670815"
---
# <a name="spchangedistributorpassword-transact-sql"></a>sp_changedistributor_password (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改分发服务器的密码。 此存储过程在分发服务器上的任何数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_changedistributor_password [ @password= ] 'password'   
```  
  
## <a name="arguments"></a>参数  
 [  **@password=**] **'***密码*****  
 是的新密码。 *密码*是**sysname**，无默认值。 如果分发服务器是本地的密码**distributor_admin**更改系统登录名。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_changedistributor_password**用于所有类型的复制。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_changedistributor_password](../../relational-databases/replication/codesnippet/tsql/sp-changedistributor-pas_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_changedistributor_password**。  
  
## <a name="see-also"></a>请参阅  
 [查看和修改复制安全设置](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [保护分发服务器](../../relational-databases/replication/security/secure-the-distributor.md)   
 [sp_adddistributor &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md)   
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
