---
title: Oracle CDC 服务 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 47759ddc-358d-405b-acb9-189ada76ea6d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8a11a67f64a40aa5fe08d375a9f11fa186c568b1
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "71298608"
---
# <a name="the-oracle-cdc-service"></a>Oracle CDC 服务

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Oracle CDC 服务是运行 xdbcdcsvc.exe 程序的一种 Windows 服务。 Oracle CDC 服务可配置为在同一台计算机上运行多个 Windows 服务，每个服务都使用不同的 Windows 服务名称。 在单个计算机上创建多个 Oracle CDC Windows 服务通常是为了在它们之间或在每个服务需要使用不同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例时实现更好的隔离。  
  
 Oracle CDC 服务是使用 Oracle CDC 服务配置控制台创建的，或者是通过内置于 xdbcdcsvc.exe 程序中的命令行接口定义的。 在这两种情况中，创建的每个 Oracle CDC 服务都与单个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例相关联（可能使用 **AlwaysOn** 安装程序被群集或镜像），并且连接信息（连接字符串和访问凭据）是服务配置的一部分。  
  
 在某一 Oracle CDC 服务启动时，它将尝试连接到其关联的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，获取它需要处理的 Oracle CDC 实例的列表，并且执行初始环境验证。 服务启动期间出现的错误以及任何开始/停止信息始终写入 Windows 应用程序事件日志。 在建立与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的连接时，所有错误和信息消息都写入 **实例的 MSXDBCDC 数据库的** dbo.xdbcdc_trace [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中。 在启动期间执行的检查之一是验证没有具有相同名称的其他 Oracle CDC 服务当前正在工作。 如果具有相同名称的某一服务当前与其他计算机连接，则 Oracle CDC 服务将进入一个等待循环，并且等待其他服务断开连接，之后继续处理 Oracle CDC 工作。  
  
 在该 Oracle CDC 服务通过所有启动验证后，它将检查任何启用的 Oracle CDC 实例的 MSXDBCDC 数据库中的 **dbo.xdbcdc_databases** 表。 对于每个已启用的 Oracle CDC 实例，该服务将启动一个子进程来处理该 Oracle CDC 实例。  
  
 在某一 Oracle CDC 实例启动时，它将访问与该 CDC 实例同名的 SQL Server CDC 数据库，并且从以前的运行中检索其状态。 它还会验证一切都正常运行。 然后，它将恢复处理更改；读取 Oracle 事务日志并且写入对 CDC 数据库的更改。  
  
 Oracle CDC 服务将定期监视 MSXDBCDC 数据库中的 **dbo.xdbcdc_tables** 表，以便确定是否存在对任何 Oracle CDC 实例配置的任何配置更改。 如果找到了更改，Oracle CDC 服务会通知 Oracle CDC 实例它应该检查其配置是否有更改。 大多数配置更改（例如添加和删除捕获实例）可在启用 Oracle CDC 实例时应用，其他更改则要求重新启动 Oracle CDC 实例。  
  
 当使用 Oracle CDC 设计器控制台时，会自动检测到更改。 在使用 SQL 直接更新 Oracle CDC 配置时，应该为 Oracle CDC 服务调用以下过程以便通知配置更改：  
  
```sql
DECLARE @dbname nvarchar(128) = 'HRcdc'  
EXECUTE [MSXDBCDC].[dbo].[xdbcdc_update_config_version] @dbname  
GO  
  
```  
  
 Oracle CDC 实例进程在系统表 **cdc.xdbcdc_state** 中更新其状态，并且将错误信息写入 **cdc.xdbcdc_trace** 表。 **xdbcdc_state** 表用于监视 Oracle CDC 实例的状态。 它提供最新的状态、不同的计数器（例如从 Oracle 读取的更改数、写入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的更改数、提交的写入事务的数目以及尚在传输中的事务的当前数目）和延迟指示。  
  
 Oracle CDC 实例配置保存在 **cdc.xdbcdc_config** 表中，该表是 Oracle CDC 设计器控制台使用的表。 因为在目标 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例和 CDC 数据库中找到了某一 Oracle CDC 实例的整个配置，所以，可以为该 Oracle CDC 实例创建 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 部署脚本。 这是使用 Oracle CDC 服务配置和 Oracle CDC 设计器控制台实现的。  
  
## <a name="security-considerations"></a>安全注意事项  
 下面介绍使用 Oracle CDC 服务时需遵守的安全要求。  
  
### <a name="protection-of-source-oracle-data"></a>源 Oracle 数据的保护  
 Oracle CDC 服务不要求对 Oracle 源数据的访问权限，并且通过确保日志挖掘凭据不对客户 Oracle 表提供 SELECT 权限，对 Oracle CDC 服务进行保护。  
  
### <a name="protection-of-source-oracle-change-data"></a>源 Oracle 更改数据的保护  
 向 Oracle CDC 服务提供日志挖掘凭据，允许该服务捕获对 Oracle 数据库中任何表进行的更改。 更改数据不具有一般表所具有的粒度访问权限，因此，访问更改表将绕过内置的 Oracle 数据访问控制。  
  
 捕获的源 Oracle 表将在 CDC 数据库中具有含相同架构和表名称的空的镜像表。 捕获的数据存储于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 捕获实例中，并且提供与为从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库捕获的更改相同的保护。 若要获取对与捕获实例关联的更改数据的访问，必须为用户授予关联镜像表中的所有捕获列的选择访问权限。 此外，如果在创建捕获实例时指定了访问控制角色，调用者还必须是指定访问控制角色的成员。 所有数据库用户可通过公共角色访问用于访问元数据的其他常规变更数据捕获功能，但返回的元数据访问通常是使用基础源表的选择访问权限以及任何定义的访问控制角色成员身份控制的。  
  
 这意味着具有 **sysadmin** 固定服务器角色或 **db_owner** 固定数据库角色的用户对捕获的数据具有（默认的）完全访问权限，并且可通过访问控制角色或通过授予对捕获的列的选择访问权限授予进一步的访问权限。  
  
### <a name="protection-of-source-oracle-log-mining-credentials"></a>源 Oracle 日志挖掘凭据的保护  
 在 CDC 数据库的 cdc.xdbcdc_config 表中存储的 Oracle CDC 服务配置包含日志挖掘用户名及其关联的密码。  
  
 通过具有使用以下命令自动创建的固定名称 `xdbcdc_asym_key` 的非对称密钥，以加密方式存储日志挖掘密码：  
  
```sql
USE [<cdc-database-name>]  
CREATE ASYMMETRIC KEY xdbcdc_asym_key  
    WITH ALGORITHM = RSA_1024  
    ENCRYPTION BY PASSWORD = '<cdc-database-name><asym-key-password>'  
  
```  
  
 如果使用不同的算法，则可以删除此密钥，并且可以创建具有相同名称且使用相同密码加密的新密钥。  
  
 非对称密钥密码是保存在路径 **HKLM\Software\Microsoft\XDBCDCSVC\\<service-name>** 下的注册表中的主密码。 只有本地管理员和 Oracle CDC Windows 服务帐户才能访问该密钥。 该密钥包含存储了非对称密钥密码的加密的二进制值 **AsymmetricKeyPassword** 。 为了能够访问 Oracle 日志挖掘凭据，需要对此注册表项的访问权限。  
  
 若要使用 ENCRYPTION BY PASSWORD 子句，该密码必须满足针对运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的计算机的 Windows 密码策略要求。 这是通过根据该策略选择非对称密钥密码来实现的。  
  
 如果丢失了该非对称密钥密码，则各 Oracle CDC 实例的日志挖掘凭据必须再次在 Oracle CDC 服务设计器中指定。  
  
 在 CDC 服务检测到不具有此非对称密钥的 Oracle 实例 CDC 数据库时，或者在该密钥存在但密码不匹配时，将自动在 CDC 数据库中创建非对称密钥。  
  
### <a name="oracle-cdc-service-windows-service-account"></a>Oracle CDC 服务 Windows 服务帐户  
 用于 Oracle CDC Windows 服务的服务帐户不要求任何附加权限。 此帐户必须能够使用 Oracle Native Client API 和 SQL Server Native Client ODBC API。 它还需要能够访问注册表中的服务配置密钥（此 CDC 服务配置控制台为此设置 ACL）。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [高可用性支持](../../integration-services/change-data-capture/high-availability-support.md)  
  
-   [针对 CDC 服务的 SQL Server 连接所需权限](../../integration-services/change-data-capture/sql-server-connection-required-permissions-for-the-cdc-service.md)  
  
-   [用户角色](../../integration-services/change-data-capture/user-roles.md)  
  
-   [使用 Oracle CDC 服务](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md)  
  
## <a name="see-also"></a>另请参阅  
 [如何管理本地 CDC 服务](../../integration-services/change-data-capture/how-to-manage-a-local-cdc-service.md)   
 [管理 Oracle CDC 服务](../../integration-services/change-data-capture/manage-an-oracle-cdc-service.md)  
  
  
