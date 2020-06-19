---
title: cross db ownership chaining 服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- cross-database ownership chaining
- cross db ownership chaining option
- chaining ownership
ms.assetid: 7b2d49f2-b91c-4aee-a52b-6cc49bed03af
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: cfb768065cc0aa2aaa7aed0f996b18e46f1da7ba
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935418"
---
# <a name="cross-db-ownership-chaining-server-configuration-option"></a>cross db ownership chaining 服务器配置选项
  使用 cross db ownership chaining  选项可以为 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例配置跨数据库所有权链。  
  
 此服务器选项使您能够在数据库级别控制跨数据库所有权链接，或者允许在所有数据库中启用跨数据库所有权链接：  
  
-   如果实例的 **cross db ownership chaining** 为关（设置为 0），将禁用所有数据库的跨数据库所有权链接。  
  
-   如果实例的 **cross db ownership chaining** 为开（设置为 1），将启用所有数据库的跨数据库所有权链接。  
  
-   可以使用 ALTER DATABASE 语句的 SET 子句为各个数据库设置跨数据库所有权链接。 如果正在创建新的数据库，则可以使用 CREATE DATABASE 语句设置新数据库的跨数据库所有权链接选项。  
  
     建议不要将 **cross db ownership chaining** 设置为 1，除非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例所驻留的所有数据库都必须参与跨数据库所有权链接，并且你了解此设置隐含的安全问题。  
  
## <a name="controlling-cross-database-ownership-chaining"></a>控制跨数据库所有权链接  
 在打开或关闭跨数据库所有权链接之前，请注意下列事项：  
  
-   只有 **sysadmin** 固定服务器角色成员能够启用或禁用跨数据库所有权链接。  
  
-   关闭生产服务器的跨数据库所有权链接之前，应全面测试所有应用程序（包括第三方应用程序）以确保更改不会影响应用程序功能。  
  
-   如果使用 **sp_configure** 指定 RECONFIGURE，则在服务器运行时可以更改 **cross db ownership chaining**选项。  
  
-   如果有数据库需要跨数据库所有权链接，建议使用 **sp_configure** 为实例禁用 **cross db ownership chaining**选项；然后使用 ALTER DATABASE 语句启用需要此功能的各个数据库的跨数据库所有权链接。  
  
## <a name="see-also"></a>另请参阅  
 [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql)   
 [CREATE DATABASE (SQL Server Transact-SQL)](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE (Transact-SQL)](/sql/t-sql/language-elements/reconfigure-transact-sql)  
  
  
