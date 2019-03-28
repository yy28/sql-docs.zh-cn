---
title: sp_syspolicy_configure (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syspolicy_configure
- sp_syspolicy_configure_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syspolicy_configure
ms.assetid: 70c10922-9345-4190-ba69-808a43f760da
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: b9ae7fdde89c9f927fbc56a9ca395138c264e931
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58532109"
---
# <a name="spsyspolicyconfigure-transact-sql"></a>sp_syspolicy_configure (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  配置基于策略的管理设置，例如，是否启用基于策略的管理。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_syspolicy_configure [ @name = ] 'name'  
    , [ @value = ] value  
```  
  
## <a name="arguments"></a>参数  
`[ @name = ] 'name'` 是你想要配置的名称。 *名称*是**sysname**且是必需的并且不能为 NULL 或空字符串。  
  
 *名称*可以是任何以下值：  
  
-   'Enabled'-确定是否启用基于策略的管理。  
  
-   'HistoryRetentionInDays' - 指定策略评估历史纪录应保留的天数。 如果设置为 0，则不会自动删除历史纪录。  
  
-   'LogOnSuccess' - 指定基于策略的管理是否记录成功的策略评估。  
  
`[ @value = ] value` 是与为指定的值相关联的值*名称*。 *值*是**sql_variant**，和是必需的。  
  
-   如果为指定 'Enabled'*名称*，可以使用以下值之一：  
  
    -   0 = 禁用基于策略的管理。  
  
    -   1 = 启用基于策略的管理。  
  
-   如果为指定 'historyrententionindays '，则*名称*，指定一个整数值的天数。  
  
-   如果为指定 'LogOnSuccess'*名称*，可以使用以下值之一：  
  
    -   0 = 只记录失败的策略评估。  
  
    -   1 = 记录成功和失败的策略评估。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 您必须在 msdb 系统数据库的上下文中运行 sp_syspolicy_configure。  
  
 若要查看这些设置的当前值，请查询 msdb.dbo.syspolicy_configuration 系统视图。  
  
## <a name="permissions"></a>权限  
 要求具有 PolicyAdministratorRole 固定数据库角色的成员身份。  
  
> [!IMPORTANT]  
>  可能的凭据提升：PolicyAdministratorRole 角色的用户可以创建服务器触发器并计划策略执行，这可能会影响的实例的[!INCLUDE[ssDE](../../includes/ssde-md.md)]。 例如，PolicyAdministratorRole 角色中的用户可以创建一个策略，它可能会禁止在[!INCLUDE[ssDE](../../includes/ssde-md.md)]中创建大多数对象。 由于此可能的凭据提升，应仅向可信任其控制的配置的用户授予 PolicyAdministratorRole 角色[!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
## <a name="examples"></a>示例  
 下面的示例启用基于策略的管理。  
  
```  
EXEC msdb.dbo.sp_syspolicy_configure @name = N'Enabled'  
, @value = 1;  
  
GO  
```  
  
 下面的示例将策略评估保持期设置为 14 天。  
  
```  
EXEC msdb.dbo.sp_syspolicy_configure @name = N'HistoryRetentionInDays'  
, @value = 14;  
  
GO  
```  
  
 下面的示例将基于策略的管理配置为成功和失败的策略评估均记录。  
  
```  
EXEC msdb.dbo.sp_syspolicy_configure @name = N'LogOnSuccess'  
, @value = 1;  
  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [基于策略的管理存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)   
 [sp_syspolicy_set_config_enabled &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-set-config-enabled-transact-sql.md)   
 [sp_syspolicy_set_config_history_retention &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-set-config-history-retention-transact-sql.md)   
 [sp_syspolicy_set_log_on_success &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-set-log-on-success-transact-sql.md)  
  
  
