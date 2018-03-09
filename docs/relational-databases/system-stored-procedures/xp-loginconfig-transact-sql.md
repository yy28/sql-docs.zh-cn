---
title: "xp_loginconfig (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- xp_loginconfig_TSQL
- xp_loginconfig
dev_langs:
- TSQL
helpviewer_keywords:
- xp_loginconfig
ms.assetid: d380e799-2857-408a-bcbf-5e73a8e6aa5a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c3e070b1a6ba44a1f2a9c626745c0c7543446095
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="xploginconfig-transact-sql"></a>xp_loginconfig (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  报告 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的登录安全配置。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
xp_loginconfig ['config_name']  
```  
  
## <a name="arguments"></a>参数  
  *config_name*   
 要显示的配置值。 如果*config_name*是未指定，报告所有配置值。 *config_name*是**sysname**，默认值为 NULL，并且可以为这些值之一。  
  
|值|Description|  
|-----------|-----------------|  
|**登录模式**|登录安全模式。 可能的值为**混合**和**Windows 身份验证**。<br /><br /> 替换为：<br /><br /> `SELECT SERVERPROPERTY('IsIntegratedSecurityOnly'); GO`|  
|**默认的登录名**|信任连接的授权用户的默认 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录 ID 名（用于无匹配登录名的用户）。 默认的登录名是**来宾**。 提供此值是为了向后兼容。|  
|**默认域**|信任连接的网络用户的默认 Windows 域名。 默认域是运行 Windows 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机所属的域。 提供此值是为了向后兼容。|  
|**审核级别**|审核级别。 可能的值为**无**，**成功**，**失败**，和**所有**。 审核将写入错误日志和 Windows 事件查看器中。|  
|**设置主机名**|指示在客户端登录记录中是否用 Windows 网络用户名替换主机名。 可能的值为**true**或**false**。 如果此设置，网络用户名称出现在输出中从**sp_who**。|  
|**映射 _**|报告将哪些特殊 Windows 字符映射为有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 下划线字符 (_)。 可能的值为**域分隔符**（默认值）、**空间**， **null**，或任何单个字符。 提供此值是为了向后兼容。|  
|**映射 $**|报告将哪些特殊 Windows 字符映射为有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 美元符号字符 ($)。 可能的值为**域分隔符**，**空间**， **null**，或任何单个字符。 默认值是**空间**。 提供此值是为了向后兼容。|  
|**映射 #**|报告将哪些特殊 Windows 字符映射为有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数字符号字符 (#)。 可能的值为**域分隔符**，**空间**， **null**，或任何单个字符。 默认值为连字符。 提供此值是为了向后兼容。|  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**sysname**|配置值|  
|**配置值**|**sysname**|配置值设置|  
  
## <a name="remarks"></a>注释  
 **xp_loginconfig**无法用于设置配置值。  
  
 若要设置登录模式和审核级别，请使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
## <a name="permissions"></a>Permissions  
 在需要的 CONTROL 权限**master**数据库。  
  
## <a name="examples"></a>示例  
  
### <a name="a-how-to-report-all-configuration-values"></a>A. 如何报告所有配置值  
 下例将显示当前配置的所有设置。  
  
```  
EXEC xp_loginconfig;  
GO  
```  
  
### <a name="b-how-to-report-a-specific-configuration-value"></a>B. 如何报告特定配置值  
 以下示例仅显示登录模式的设置。  
  
```  
EXEC xp_loginconfig 'login mode';  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_denylogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_grantlogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_revokelogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [xp_logininfo &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
