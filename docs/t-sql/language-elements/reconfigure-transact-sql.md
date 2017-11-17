---
title: "RECONFIGURE (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 05/20/2016
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RECONFIGURE
- RECONFIGURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- reconfiguring configuration options
- configuration options [SQL Server], reconfiguring
- updating configuration options
- RECONFIGURE, RECONFIGURE statement
- RECONFIGURE
- RECONFIGURE, WITH OVERRIDE statement
ms.assetid: 2e6e4eeb-b70b-4f45-a253-28ac4e595d75
caps.latest.revision: 50
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 32039a4077f028a078e9265c6d18f5cbb6187e3f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="reconfigure-transact-sql"></a>RECONFIGURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更新当前配置的值 ( **config_value**中的列**sp_configure**结果集) 的配置选项的更改与**sp_configure**系统存储的过程。 因为某些配置选项需要服务器停止并重新启动以更新当前正在运行的值，重新配置不会始终更新当前正在运行的值 ( **run_value**中的列**sp_configure**结果集) 的更改的配置值。    
    
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>语法    
    
```    
    
RECONFIGURE [ WITH OVERRIDE ]    
```    
    
## <a name="arguments"></a>参数    
 RECONFIGURE    
 指定如果配置设置不需要服务器停止并重新启动，则更新当前运行的值。 RECONFIGURE 还检查无效任一值的新配置值 (例如，不存在于一个排序顺序值**syscharsets**) 或推荐的值。 对于那些不需要服务器停止并重新启动的配置选项，其当前运行的值和当前配置的值在指定 RECONFIGURE 之后应当相同。    
    
 WITH OVERRIDE    
 禁用检查 （不是有效的值或者为推荐的值） 的配置值**恢复间隔**高级配置选项。    
    
 几乎任何配置选项可通过使用 WITH OVERRIDE 选项，但是某些致命错误，则仍可以避免重新配置。 例如，**最小服务器内存**配置选项不能配置为某个值中指定的值大于**最大服务器内存**配置选项。
      
## <a name="remarks"></a>注释    
 **sp_configure**不接受新的配置选项值，在每个配置选项有案可稽的有效范围内。    
    
 不允许在显式或隐式事务中使用 RECONFIGURE。 同时对多个选项进行重新配置时，如果任意重新配置操作失败，所有重新配置操作都将无效。    
    
 当重新配置资源调控器，请参阅的重新配置选项[ALTER RESOURCE GOVERNOR &#40;Transact SQL &#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md).    
    
## <a name="permissions"></a>Permissions    
 默认情况下，被授予 ALTER SETTINGS 权限的用户同时拥有 RECONFIGURE 权限。 **Sysadmin**和**serveradmin**固定的服务器角色隐式保存此权限。    
    
## <a name="examples"></a>示例    
 以下示例将 `recovery interval` 配置选项的上限设置为 `75` 分钟，并使用 `RECONFIGURE WITH OVERRIDE` 进行安装。 建议恢复间隔不要大于 60 分钟，并且默认情况下是不接受的。 但是，由于指定了 `WITH OVERRIDE` 选项，因此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不会检查指定的值 (`90`) 是否为 `recovery interval` 配置选项的有效值。    
    
```    
EXEC sp_configure 'recovery interval', 75'    
RECONFIGURE WITH OVERRIDE;    
GO    
```    
    
## <a name="see-also"></a>另请参阅    
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)     
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)    
    
  

