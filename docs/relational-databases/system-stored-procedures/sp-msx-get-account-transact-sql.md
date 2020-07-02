---
title: sp_msx_get_account （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_msx_get_account_TSQL
- sp_msx_get_account
dev_langs:
- TSQL
helpviewer_keywords:
- sp_msx_get_account
ms.assetid: 7b478049-e2d0-4bac-865a-b97fd1d8dfbc
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 82c26d20933562b05bb95796140dcc51bbc0777d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85734328"
---
# <a name="sp_msx_get_account-transact-sql"></a>sp_msx_get_account (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  列出有关目标服务器用于登录到主服务器的凭据的信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_msx_get_account  
```  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 返回以下结果集：  
  
|列名|类型|描述|  
|-----------------|----------|-----------------|  
|msx_connection|**int**|主服务器连接号。|  
|msx_credential_id|**int**|用于此主服务器连接的凭据的 ID。|  
|msx_credential_name|**sysname**|用于此主服务器连接的凭据的名称。|  
|msx_login_name|**nvarchar(4000)**|凭据的 Windows 用户的域名和用户名。|  
  
## <a name="remarks"></a>备注  
 如果不存在为此目标服务器指定的凭据，则返回一个空结果集。 若要设置使用该凭据，可使用 sp_msx_set_account。  
  
## <a name="permissions"></a>权限  
 要求具有 sysadmin 固定服务器角色的成员身份。  
  
## <a name="examples"></a>示例  
 下面的示例将列出此目标服务器用于登录到主服务器的凭据的信息。  
  
```  
USE msdb ;  
GO  
  
EXECUTE dbo.sp_msx_get_account ;  
GO  
```  
  
 下面是一个示例结果集：  
  
 `msx_connection msx_credential_id msx_credential_name  msx_login_name`  
  
 `-------------- ----------------- -------------------- ------------------------------`  
  
 `1              65538             MsxAccount           AdventureWorks2012\MsxAccount`  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 代理存储过程 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [&#40;Transact-sql&#41;创建凭据](../../t-sql/statements/create-credential-transact-sql.md)   
 [sp_msx_set_account &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-msx-set-account-transact-sql.md)  
  
  
