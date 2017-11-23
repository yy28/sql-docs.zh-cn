---
title: "sp_vupgrade_replication (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_vupgrade_replication_TSQL
- sp_vupgrade_replication
helpviewer_keywords: sp_vupgrade_replication
ms.assetid: d2c0ed66-07d1-4adc-82e5-a654376879bc
caps.latest.revision: "30"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d07f50261726675d921f39226cd97f9b163b1f7f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spvupgradereplication-transact-sql"></a>sp_vupgrade_replication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  升级复制服务器时由安装程序激活。 根据需要升级架构和系统数据，以支持当前产品级别上的复制。 在系统和用户数据库中创建新的复制系统对象。 此存储过程在要发生复制升级的计算机上执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_vupgrade_replication [ [@login=] 'login' ]  
    [ , [ @password= ] 'password' ]  
    [ , [ @ver_old= ] 'old_version' ]  
    [ , [ @force_remove= ] 'force_removal' ]  
    [ , [ @security_mode= ] security_mode ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@login=**] *登录*  
 在分发数据库中创建新的系统对象时使用的系统管理员登录名。 *登录名*是**sysname**，默认值为 NULL。 如果不需要此参数*security_mode*设置为**1**，即 Windows 身份验证。  
  
> [!NOTE]  
>  在升级到 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更高版本后将忽略此参数。  
  
 [  **@password=**] *密码*  
 是分发数据库中创建新的系统对象时要使用的系统管理员密码。 *密码*是**sysname**，默认值为**'** （空字符串）。 如果不需要此参数*security_mode*设置为**1**，即 Windows 身份验证。  
  
> [!NOTE]  
>  在升级到 SQL [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更高版本后将忽略此参数。  
  
 [  **@ver_old=**] *old_version*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 不推荐使用此存储过程，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的未来版本中将删除它。  
  
 [  **@force_remove=**] *force_removal*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@security_mode=**] *security_mode*  
 在分发数据库中创建新的系统对象时要使用的登录安全模式。 *security_mode*是**位**默认值为**0**。 如果**0**，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将使用身份验证。 如果**1**，将使用 Windows 身份验证。  
  
> [!NOTE]  
>  在升级到 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更高版本后将忽略此参数。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_vupgrade_replication**升级所有类型的复制时使用。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_vupgrade_replication**。  
  
## <a name="see-also"></a>另请参阅  
 [复制存储过程 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [验证已复制的数据](../../relational-databases/replication/validate-replicated-data.md)  
  
  
