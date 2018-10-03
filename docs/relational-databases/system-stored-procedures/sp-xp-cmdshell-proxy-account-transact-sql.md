---
title: sp_xp_cmdshell_proxy_account (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_xp_cmdshell_proxy_account
- sp_xp_cmdshell_proxy_account_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_xp_cmdshell_proxy_account
- xp_cmdshell
ms.assetid: f807c373-7fbc-4108-a2bd-73b48a236003
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 83525324b328a688713418835b353e4a72892a0b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47781645"
---
# <a name="spxpcmdshellproxyaccount-transact-sql"></a>sp_xp_cmdshell_proxy_account (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  创建的代理凭据**xp_cmdshell**。  
  
> [!NOTE]  
>  **xp_cmdshell**默认处于禁用状态。 若要启用**xp_cmdshell**，请参阅[xp_cmdshell 服务器配置选项](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_xp_cmdshell_proxy_account [ NULL | { 'account_name' , 'password' } ]  
```  
  
## <a name="arguments"></a>参数  
 NULL  
 指定应删除的代理凭据。  
  
 *account_name*  
 指定要成为代理的 Windows 登录名。  
  
 *password*  
 指定 Windows 帐户的密码。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>备注  
 将调用代理凭据 **# # xp_cmdshell_proxy_account # #**。  
  
 当使用 NULL 选项执行**sp_xp_cmdshell_proxy_account**删除代理凭据。  
  
## <a name="permissions"></a>Permissions  
 需要 CONTROL SERVER 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-creating-the-proxy-credential"></a>A. 创建代理凭据  
 以下示例显示如何使用密码 `ADVWKS\Max04` 为 Windows 帐户创建名为 `ds35efg##65` 的代理凭据。  
  
```  
EXEC sp_xp_cmdshell_proxy_account 'ADVWKS\Max04', 'ds35efg##65';  
GO  
```  
  
### <a name="b-dropping-the-proxy-credential"></a>B. 删除代理凭据  
 以下示例从凭据存储区中删除代理凭据。  
  
```  
EXEC sp_xp_cmdshell_proxy_account NULL;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [xp_cmdshell &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/xp-cmdshell-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.credentials (Transact-SQL)](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [安全存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  
