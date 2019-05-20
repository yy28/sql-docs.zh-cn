---
title: 使用服务 SID 授予对 SQL Server 中的服务的访问权限 | Microsoft Docs
author: randomnote1
ms.author: dareist
ms.date: 05/02/2019
ms.topic: conceptual
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.openlocfilehash: 1a0bd129fc535b53d8d19ad76f99f3a86ba10c11
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65135233"
---
# <a name="using-service-sids-to-grant-permissions-to-services-in-sql-server"></a>使用服务 SID 授予对 SQL Server 中的服务的访问权限

SQL Server 使用[每个服务的安全标识符 (SID)](https://support.microsoft.com/help/2620201/sql-server-uses-a-service-sid-to-provide-service-isolation) 来允许直接授予对特定服务的访问权限。 SQL Server 使用此方法来授予对引擎和代理服务的访问权限（分别为 NT SERVICE\MSSQL$<InstanceName> 和 NT SERVICE\SQLAGENT$<InstanceName>）。 若使用此方法，这些服务只能在服务运行时访问数据库引擎。

授予对其他服务的访问权限时，可以使用相同的方法。 使用服务 SID 可以消除管理和维护服务帐户的开销，并对授予系统资源的权限提供更严格、更精细的控制。

可以使用服务 SID 的服务示例包括：

- System Center Operations Manager 运行状况服务 (NT SERVICE\HealthService)
- Windows Server 故障转移群集 (WSFC) 服务 (NT SERVICE\ClusSvc)

默认情况下，某些服务没有服务 SID。 必须使用 [SC.exe](https://docs.microsoft.com/windows/desktop/services/configuring-a-service-using-sc) 创建服务 SID。 Microsoft System Center Operations Manager 管理员已采用[此方法](https://kevinholman.com/2016/08/25/sql-mp-run-as-accounts-no-longer-required/)授予对 SQL Server 中的 HealthService 的访问权限。

创建并确认了服务 SID 后，必须授予它在 SQL Server 中的权限。 使用 [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 或查询创建 Windows 登录名，从而完成权限授予。 创建登录名后，就可以像其他登录名一样授予其权限、将其添加到角色以及映射到数据库。

> [!TIP]
> 如果收到错误 `Login failed for user 'NT AUTHORITY\SYSTEM'`，请验证所需服务的服务 SID 是否存在、是否在 SQL Server 中创建了服务 SID 登录名，以及是否已在 SQL Server 中为该服务 SID 授予了相应权限。

## <a name="security"></a>Security

### <a name="eliminate-service-accounts"></a>消除服务帐户

传统上，服务帐户已用于允许服务登录到 SQL Server。 由于必须维护和定期更新服务帐户密码，因此服务帐户会增加额外的管理复杂性。 此外，在实例中执行操作时，个人可能会尝试使用服务帐户凭据来掩盖其活动。

### <a name="granular-permissions-to-system-accounts"></a>系统帐户的具体权限

系统历来通过为 [LocalSystem](https://msdn.microsoft.com/library/windows/desktop/ms684190)（[NT AUTHORITY\SYSTEM，语言为 en-us](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions#Localized_service_names)）或 [NetworkService](https://docs.microsoft.com/windows/desktop/Services/networkservice-account)（[NT AUTHORITY\NETWORK SERVICE，语言为 en-us](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions?#Localized_service_names)）帐户创建登录名并授予这些登录名权限，来授予系统帐户权限。 此方法在以系统帐户运行的 SQL 中授予任何进程或服务权限。

使用服务 SID 允许对特定服务授予权限。 该服务在运行时只能访问已授予权限的资源。 例如，如果 `HealthService` 作为 `LocalSystem` 运行并被授予 `View Server State`，则 `LocalSystem` 帐户仅在 `HealthService` 的上下文中运行时才具有对 `View Server State` 的权限。 如果任何其他进程尝试像 `LocalSystem` 一样访问 SQL 的服务器状态，则将被拒绝访问。

## <a name="examples"></a>示例

### <a name="a-create-a-service-sid"></a>A. 创建服务 SID

以下 PowerShell 命令将在 System Center Operations Manager 运行状况服务上创建服务 SID。

```PowerShell
sc.exe --% sidtype "HealthService" unrestricted
```

> [!IMPORTANT]
> `--%` 告诉 PowerShell 停止解析命令的其余部分。 这在使用旧版命令和应用程序时很有用。

### <a name="b-query-a-service-sid"></a>B. 查询服务 SID

要检查服务 SID 或确保存在服务 SID，请在 PowerShell 中执行以下命令。

```PowerShell
sc.exe --% qsidtype "HealthService"
```

> [!IMPORTANT]
> `--%` 告诉 PowerShell 停止解析命令的其余部分。 这在使用旧版命令和应用程序时很有用。

### <a name="c-add-a-newly-created-service-sid-as-a-login"></a>C. 添加新创建的服务 SID 作为登录名

以下示例使用 T-SQL 为 System Center Operations Manager 运行状况服务创建登录名。

```SQL
CREATE LOGIN [NT SERVICE\HealthService] FROM WINDOWS
GO
```

### <a name="d-add-an-existing-service-sid-as-a-login"></a>D. 添加现有服务 SID 作为登录名

以下示例使用 T-SQL 为群集服务创建登录名。 授予群集服务权限可避免向系统帐户授予过多权限。

```SQL
CREATE LOGIN [NT SERVICE\ClusSvc] FROM WINDOWS
GO
```

### <a name="e-grant-permissions-to-a-service-sid"></a>E. 授予服务 SID 权限

向群集服务授予管理可用性组所需的权限。

```SQL
GRANT ALTER ANY AVAILABILITY GROUP TO 'NT SERVICE\ClusSvc'
GO

GRANT CONNECT SQL TO 'NT SERVICE\ClusSvc'
GO

GRANT VIEW SERVER STATE TO 'NT SERVICE\ClusSvc'
GO
```

## <a name="next-steps"></a>后续步骤

有关服务 SID 结构的详细信息，请参阅 [SERVICE_SID_INFO 结构](https://docs.microsoft.com/windows/desktop/api/winsvc/ns-winsvc-_service_sid_info)。

了解[创建登录名](https://docs.microsoft.com/sql/t-sql/statements/create-login-transact-sql)时可用的其他选项。

要将基于角色的安全性与服务 SID 一起使用，请参阅 SQL Server 中的[创建角色](https://docs.microsoft.com/sql/t-sql/statements/create-role-transact-sql)。

了解向 SQL Server 中的服务 SID [授予权限](https://docs.microsoft.com/sql/t-sql/statements/grant-transact-sql)的不同方法。
