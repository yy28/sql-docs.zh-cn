---
title: sp_xp_cmdshell_proxy_account （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e908d0bfb70e60330ce47377a8537ebe25f80f09
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827461"
---
# <a name="sp_xp_cmdshell_proxy_account-transact-sql"></a>sp_xp_cmdshell_proxy_account (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  为**xp_cmdshell**创建代理凭据。  
  
> [!NOTE]  
>  默认情况下，禁用**xp_cmdshell** 。 若要启用**xp_cmdshell**，请参阅[Xp_cmdshell 服务器配置选项](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_xp_cmdshell_proxy_account [ NULL | { 'account_name' , 'password' } ]  
```  
  
## <a name="arguments"></a>参数  
 Null  
 指定应删除的代理凭据。  
  
 *account_name*  
 指定要成为代理的 Windows 登录名。  
  
 *password*  
 指定 Windows 帐户的密码。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>备注  
 代理凭据将称为 **# #xp_cmdshell_proxy_account # #**。  
  
 当使用 NULL 选项执行时， **sp_xp_cmdshell_proxy_account**会删除代理凭据。  
  
## <a name="permissions"></a>权限  
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
  
## <a name="see-also"></a>另请参阅  
 [xp_cmdshell &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/xp-cmdshell-transact-sql.md)   
 [&#40;Transact-sql&#41;创建凭据](../../t-sql/statements/create-credential-transact-sql.md)   
 [sys.databases &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [&#40;Transact-sql&#41;系统存储过程](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [安全存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  
