---
title: 用户角色的变更数据捕获 Service for Oracle by Attunity |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: be0ec384-e03b-4483-96ca-02b289804d6a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b62f749bf308684a5d47386011339505b8a23bb0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48222887"
---
# <a name="user-roles-for-change-data-capture-service-for-oracle-by-attunity"></a>使用 Change Data Capture Service for Oracle by Attunity 的角色
  本节介绍 Change Data Capture Service for Oracle by Attunity 的用户角色。 介绍的角色包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库角色、Windows 角色或 Oracle 数据库角色。  
  
## <a name="windows-user-roles"></a>Windows 用户角色  
 下面的内容介绍 Oracle CDC 服务所使用的 Windows 用户角色。  
  
### <a name="computer-administrator-oracle-cdc-service"></a>计算机管理员：Oracle CDC 服务  
 计算机管理员是负责创建和维护计算机上的 CDC 服务的 Windows 用户。 此用户必须属于本地计算机管理员组。  
  
 Oracle CDC 服务计算机管理员执行的任务包括：  
  
-   安装 Oracle CDC 服务软件  
  
-   创建 Oracle CDC Windows 服务  
  
-   设置与目标 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的 CDC 服务连接（连接字符串和凭据）  
  
-   确保使用 CDC 服务主密码来保护 Oracle 日志挖掘凭据  
  
-   删除 CDC 服务 Windows 服务  
  
-   卸载 Oracle CDC 服务软件  
  
-   维护 Oracle CDC 服务软件（例如，安装更新）  
  
-   启动和停止 CDC 服务 Windows 服务  
  
 在使用 Microsoft 故障转移群集之类的高可用性配置时，计算机管理员必须具有其他职责和权限，例如：  
  
-   所有群集节点上 Oracle CDC 服务软件的安装和维护。  
  
-   为不同群集节点上的 CDC 服务的 Windows 服务定义一般群集服务资源。  
  
-   充当授权为安装了 Oracle CDC 服务的计算机上的管理员的计算机管理员。 此人士安装 Oracle CDC 服务并且使用 CDC 服务配置控制台为本地计算机上的 Oracle 配置 CDC 服务。  
  
### <a name="service-account-oracle-cdc-service"></a>服务帐户：Oracle CDC 服务  
 这是 Oracle CDC 服务的 Windows 服务帐户，作为运行 Oracle CDC 服务的 Windows 帐户（服务帐户）。  
  
 该服务帐户唯一必需的权限是能够使用 Oracle 客户端和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本机客户端 ODBC 访问接口。 此帐户无需访问文件，除非特定的访问接口需要（例如，如果 Oracle 客户端连接字符串引用 **tnsnames.ora** 文件中的 Oracle 数据库实例，则该服务帐户必须可读访问该文件）。  
  
 在 Windows Vista 或 Windows Server 2008 上创建 Oracle CDC 服务时，默认服务帐户是 NETWORK SERVICE 帐户。  
  
 在 Windows 7、Windows Server 2008 R2 和更高版本中，默认服务帐户是 NT Service\\<service-name>。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 运行在其他计算机上或者是群集 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例并且服务需要使用 Windows 身份验证连接到目标 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时，该服务帐户应该是域帐户。  
  
## <a name="sql-server-user-roles"></a>SQL Server 用户角色  
 下面的内容介绍 Oracle CDC 服务所使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户角色。  
  
### <a name="oracle-cdc-service-administrator"></a>Oracle CDC 服务管理员  
 CDC 服务管理员是对目标 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中的 Oracle CDC 服务项目具有完全控制权限的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户。 CDC 服务管理员使用 Oracle CDC 设计器控制台来设计 Oracle CDC 实例。  
  
 应向 CDC 服务管理员授予 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 固定服务器角色 **public** 和 **dbcreator**。  
  
 CDC 服务管理员执行的任务包括：  
  
-   准备 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例以便承载 Oracle CDC 实例（即 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库）。 在此任务中，将在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中创建一个称为 MSXDBCDC 的特殊数据库。  
  
-   创建 Oracle CDC 实例 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库。 任务包括为 CDC 启用新创建的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库，这要求 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] system administrator (**sysadmin**)。  
  
-   设计 Oracle CDC 实例。 此任务包括提供有关源 Oracle 数据库和捕获表的信息，这要求 Oracle 数据库管理员。  
  
-   随着时间的推移维护 Oracle CDC 实例，其中包括添加/删除捕获实例和更新配置。  
  
-   启用或禁用 Oracle CDC 实例。  
  
-   监视 Oracle CDC 实例的状态。  
  
-   解决影响 Oracle CDC 实例的问题。  
  
 CDC 服务管理员是（至少最初是）与 Oracle CDC 实例相关联的 **CDC 数据库的** db_owner [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 固定数据库角色。 这使得 CDC 服务管理员有权访问在 CDC 数据库中存储的更改数据。 一旦创建，CDC 数据库的 **db_owner** 角色可以分配给其他可执上面所列所有任务（准备 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例并创建另一个 Oracle CDC 实例除外）的用户。  
  
 CDC 服务管理员无需知道在创建 Oracle CDC Windows 服务时指定的主密码。  
  
### <a name="system-administrator"></a>系统管理员  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统管理员是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户，并且应被授予与 Oracle CDC 服务关联的 **实例上的固定服务器** sysadmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 角色。  
  
 只有一个由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统管理员执行的 Oracle CDC 特定的任务，该任务是为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC 启用针对 Oracle CDC 实例的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库。 此任务是在创建新的 Oracle CDC 实例时使用 Oracle CDC 设计器控制台执行的。  
  
### <a name="oracle-cdc-service-user"></a>Oracle CDC 服务用户  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC 服务帐户是一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名，Oracle CDC 服务使用该登录名对 MSXDBCDC 以及该服务处理的所有 Oracle CDC 实例（CDC 数据库）执行其工作。  
  
 应向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC 服务用户授予以下权限：  
  
-   针对服务器处理的所有 CDC 数据库的固定数据库角色 **db_dlladmin****db_datareader****db_datawriter** 的成员。  
  
-   MSXDBCDC 数据库的固定数据库角色 **db_datareader** 和 **db_datawriter** 的成员。  
  
 因为 Oracle CDC 服务使用单个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名来处理所有 CDC 数据库和 MSXDBCDC 数据库，所以，应该在所有这些数据库中映射该登录名。  
  
### <a name="oracle-cdc-change-consumer"></a>Oracle CDC 更改使用者  
 Oracle CDC 更改使用者是一种 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户，此类用户使用在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC 实例数据库的 CDC 表中存储的更改。  
  
 此用户确定通过 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC 基础结构生成的 CDC 函数访问各 CDC 表所需的用户角色。 如果在指定捕获实例时未指定任何用户角色，则对更改的访问将限制为 CDC 数据库的 **db_owner** 固定数据库角色的成员。  
  
## <a name="oracle-user-roles"></a>Oracle 用户角色  
 下面的内容介绍 Oracle CDC 服务所使用的 Oracle 用户角色。  
  
### <a name="database-administrator-dba"></a>数据库管理员 (DBA)  
 Oracle 数据库管理员 (DBA) 是 Oracle 数据库用户。 Oracle DBA 执行的任务包括：  
  
-   对源 Oracle 数据库进行设置以便在 ARCHIVELOG 模式下工作。  
  
-   设置具有所需权限的日志挖掘用户。  
  
-   为捕获表设置补充日志记录。  
  
-   帮助还原已存档的不再可用的事务日志文件，以便可以对它们进行处理。  
  
 Oracle 数据库管理员可以获取需要运行的 Oracle SQL 脚本，以便可以在运行它们之前进行评估。 Oracle 数据库管理员还可以直接从 Oracle CDC 设计器控制台运行 Oracle SQL 脚本。  
  
 如果 Oracle 数据库管理员选择使用 Oracle CDC 设计器控制台，则管理员的凭据不保存，只有使用它们的上下文（对话框）除外。  
  
 Oracle 数据库管理员与 Oracle CDC 服务管理员协调工作来配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC 实例。  
  
### <a name="log-mining-user"></a>日志挖掘用户  
 Oracle 日志挖掘用户是一种特殊的 Oracle 数据库用户，此类用户被授予访问和处理 Oracle 事务日志所需的权限。  
  
 此用户的凭据使用非对称密钥加密存储于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC 实例数据库中。 它们仅对于 Oracle CDC 服务是可访问的，对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle CDC 实例数据库所有者则无法访问。  
  
 下表描述应向日志挖掘用户授予的所需权限：  
  
-   SELECT on \<any-captured-table>  
  
-   SELECT ANY TRANSACTION  
  
-   EXECUTE on DBMS_LOGMNR  
  
-   SELECT on V$LOGMNR_CONTENTS  
  
-   SELECT on V$ARCHIVED_LOG  
  
-   SELECT on V$LOG  
  
-   SELECT on V$LOGFILE  
  
-   SELECT on V$DATABASE  
  
-   SELECT on V$THREAD  
  
-   SELECT on V$PARAMETER  
  
-   SELECT on DBA_REGISTRY  
  
-   SELECT on ALL_INDEXES  
  
-   SELECT on ALL_OBJECTS  
  
-   SELECT on DBA_OBJECTS  
  
-   SELECT on ALL_TABLES  
  
 如果无法将上述任何权限授予 V$xxx，则应向其授予 V $xxx。  
  
### <a name="schema-user"></a>架构用户  
 Oracle 架构用户是对要捕获的 Oracle 表的架构具有读访问权限的 Oracle 用户。 在使用 Oracle CDC 设计器控制台检索 Oracle 架构的列表、要捕获的表及其列、索引和密钥时此用户是必需的。  
  
 永远不会存储此用户的凭据。 每当需要这些凭据时 CDC 设计器控制台将请求这些凭据，并且将为其余的用户界面会话保存它们。  
  
  
