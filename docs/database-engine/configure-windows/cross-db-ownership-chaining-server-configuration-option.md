---
title: cross db ownership chaining 服务器配置选项 | Microsoft Docs
description: 了解如何使用 SQL Server 中的跨数据库所有权链接”选项。 查看打开或关闭跨数据库所有权链接的注意事项。
ms.custom: ''
ms.date: 08/15/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- cross-database ownership chaining
- cross db ownership chaining option
- chaining ownership
ms.assetid: 7b2d49f2-b91c-4aee-a52b-6cc49bed03af
author: markingmyname
ms.author: maghan
ms.openlocfilehash: eefc2b48f43aa91afa982775829648d76856b392
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772615"
---
# <a name="cross-db-ownership-chaining-server-configuration-option"></a>cross db ownership chaining 服务器配置选项
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  使用 cross db ownership chaining 选项可以为 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例配置跨数据库所有权链。  
  
 此服务器选项使您能够在数据库级别控制跨数据库所有权链接，或者允许在所有数据库中启用跨数据库所有权链接：  
  
-   如果实例的 **cross db ownership chaining** 为关（设置为 0），将禁用所有数据库的跨数据库所有权链接。  
  
-   如果实例的 **cross db ownership chaining** 为开（设置为 1），将启用所有数据库的跨数据库所有权链接。  
  
-   可以使用 ALTER DATABASE 语句的 SET 子句为各个数据库设置跨数据库所有权链接。 如果正在创建新的数据库，则可以使用 CREATE DATABASE 语句设置新数据库的跨数据库所有权链接选项。  
  
     建议不要将 **cross db ownership chaining** 设置为 1，除非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例所驻留的所有数据库都必须参与跨数据库所有权链接，并且你了解此设置隐含的安全问题。  

若要确定跨数据库所有权链接的当前状态，请执行以下查询：  
```sql
SELECT is_db_chaining_on, name FROM sys.databases;
```  
结果为 1 指示启用了“跨数据库所有权链接”。

## <a name="controlling-cross-database-ownership-chaining"></a>控制跨数据库所有权链接  
 在打开或关闭跨数据库所有权链接之前，请注意下列事项：  
  
-   只有 **sysadmin** 固定服务器角色成员能够启用或禁用跨数据库所有权链接。  
  
-   关闭生产服务器的跨数据库所有权链接之前，应全面测试所有应用程序（包括第三方应用程序）以确保更改不会影响应用程序功能。  
  
-   如果使用 **sp_configure** 指定 RECONFIGURE，则在服务器运行时可以更改 **cross db ownership chaining**选项。  
  
-   如果有数据库需要跨数据库所有权链接，建议使用 **sp_configure** 为实例禁用 **cross db ownership chaining**选项；然后使用 ALTER DATABASE 语句启用需要此功能的各个数据库的跨数据库所有权链接。  
  
## <a name="see-also"></a>另请参阅  
 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE (Transact-SQL)](../../t-sql/language-elements/reconfigure-transact-sql.md)  
  
  
