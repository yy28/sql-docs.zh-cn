---
title: SqlPackage.exe |Microsoft Docs
ms.prod: sql
ms.technology: ssdt
ms.date: 2018-06-27
ms.reviewer: alayu; sstein
ms.topic: conceptual
ms.assetid: 198198e2-7cf4-4a21-bda4-51b36cb4284b
author: pensivebrian
ms.author: broneill
manager: craigg
ms.openlocfilehash: 2d16e9c805f9979a53a9e8bc8c2e265e06ccbab9
ms.sourcegitcommit: 7e828cd92749899f4e1e45ef858ceb9a88ba4b6a
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 11/14/2018
ms.locfileid: "51629620"
---
# <a name="sqlpackageexe"></a>SqlPackage.exe

SqlPackage.exe 是一个命令行实用工具，可自动处理以下数据库开发任务：  
  
- [提取](#help-for-the-extract-action)：从活动的 SQL Server 或 Azure SQL 数据库创建数据库快照 (.dacpac) 文件。  
  
- [发布](#publish-parameters-properties-and-sqlcmd-variables)：增量更新数据库架构以便匹配源 .dacpac 文件的架构。 如果该数据库在服务器上不存在，则发布操作将创建它。 否则，更新现有数据库。  
  
- [导出](#export-parameters-and-properties)：将活动数据库（包括数据库架构和用户数据）从 SQL Server 或 Azure SQL 数据库导出到 BACPAC 包（.bacpac 文件）。  
  
- [导入](#import-parameters-and-properties)：将架构和表数据从 BACPAC 包导入到 SQL Server 或 Azure SQL 数据库的实例中的新用户数据库中。  
  
- [DeployReport](#deployreport-parameters-and-properties)：创建将由发布操作完成的更改的 XML 报表。  
  
- [DriftReport](#driftreport-parameters)：创建自注册数据库注册以来已对其做出的更改的 XML 报表。  
  
- [脚本](#script-parameters-and-properties)：创建 Transact-SQL 增量更新脚本，该脚本可更新目标的架构以匹配源的架构。  
  
通过 SqlPackage.exe 命令行，可以指定这些操作以及特定于操作的参数和属性。  

[下载最新版本](sqlpackage-download.md)。 有关最新版本的详细信息，请参阅[发行说明](sqlpackage-release-notes.md)。
  
## <a name="command-line-syntax"></a>命令行语法

SqlPackage.exe 使用在命令行上指定的参数、属性和 SQLCMD 变量启动指定的操作。  
  
```
SqlPackage {parameters}{properties}{SQLCMD Variables}  
```
  
### <a name="help-for-the-extract-action"></a>有关提取操作的帮助

|参数|缩写|ReplTest1|描述|
|---|---|---|---|
|**/Action:**|**/a**|Extract|指定要执行的操作。 |
|**/AccessToken:**|**/at**|{string}| 指定要在连接到目标数据库时使用的基于令牌的身份验证访问令牌。 |
|**/Diagnostics:**|**/d**|{True&#124;False}|指定诊断日志记录是否输出到控制台。 默认为 False。 |
|**/ DiagnosticsFile:**|**/df**|{string}|指定一个用于存储诊断日志的文件。 |
|**/ MaxParallelism:**|**/mp**|{int}| 指定针对数据库运行的并发操作的并行度。 默认值为 8。 |
|**/ OverwriteFiles:**|**/of**|{True&#124;False}|指定 sqlpackage.exe 是否应覆盖现有文件。 指定 false 会导致 sqlpackage.exe 在遇到现有文件时中断操作。 默认值为 True。 |
|**/Properties:**|**/p**|{PropertyName}={Value}|为特定于操作的属性指定名称值对；{PropertyName}={Value}。 请参考特定操作的帮助以便查看该操作的属性名称。 示例： sqlpackage.exe /Action： 发布 /？。 |
|**/Quiet:**|**/q**|{True&#124;False}|指定是否隐藏详细反馈。 默认为 False。 |
|**/ SourceConnectionString:**|**/ scs**|{string}|指定源数据库的有效 SQL Server/Azure 连接字符串。 如果指定了此参数，则应该独立于所有其他源参数来使用此参数。 |
|**/SourceDatabaseName:**|**/sdn**|{string}|定义源数据库的名称。 |
|**/ SourceEncryptConnection:**|**/sec**|{True&#124;False}|指定是否应该将 SQL 加密用于源数据库连接。 |
|**/SourcePassword:**|**/sp**|{string}|对于 SQL Server 身份验证方案，定义要用于访问源数据库的密码。 |
|**/ SourceServerName:**|**/ssn**|{string}|定义承载源数据库的服务器的名称。 |
|**/ SourceTimeout:**|**/st**|{int}|指定建立与源数据库的连接的超时时间（以秒为单位）。 |
|**/ SourceTrustServerCertificate:**|**/stsc**|{True&#124;False}|指定是否使用 SSL 对源数据库连接进行加密并绕过证书链来验证信任。 |
|**/SourceUser:**|**/su**|{string}|对于 SQL Server 身份验证方案，定义要用于访问源数据库的 SQL Server 用户。 |
|**/TargetFile:**|**/tf**|{string}| 指定要用作操作而不是数据库的目标的目标文件 （即.dacpac 文件）。 如果使用此参数，则其他目标参数应无效。 此参数应仅支持数据库目标的操作无效。| 
|**/TenantId:**|**/tid**|{string}|表示 Azure AD 租户 ID 或域名称。 此选项支持来宾所需或导入 Azure AD 用户，以及 Microsoft 帐户，如 outlook.com、 hotmail.com 或 live.com。 如果省略此参数，则将使用 Azure AD 的默认租户 ID，假定已经过身份验证的用户是此 AD 本机用户。 但是，在这种情况下任何来宾或导入的用户和/或在此 Azure AD 中托管的 Microsoft 帐户不支持，并且该操作将失败。 <br/> 有关 Active Directory 通用身份验证的详细信息，请参阅[SQL 数据库和 SQL 数据仓库 （对 MFA 的 SSMS 支持） 的通用身份验证](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)。|
|**/ UniversalAuthentication:**|**/ua**|{True&#124;False}|指定是否应使用通用身份验证。 设置为 True 时，支持 MFA 激活的交互式身份验证协议。 此选项还可用于 Azure AD 身份验证，而无需 MFA，使用交互式协议要求用户输入其用户名和密码或集成身份验证 （Windows 凭据）。 没有 Azure AD 身份验证时 /UniversalAuthentication 设置为 True，可以指定在 SourceConnectionString (/ scs)。 Azure AD 身份验证时 /UniversalAuthentication 设置为 False 时，必须指定在 SourceConnectionString (/ scs)。 <br/> 有关 Active Directory 通用身份验证的详细信息，请参阅[SQL 数据库和 SQL 数据仓库 （对 MFA 的 SSMS 支持） 的通用身份验证](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)。|

### <a name="properties-specific-to-the-extract-action"></a>特定于提取操作属性

|“属性”|ReplTest1|描述|
|---|---|---|
|**/p:**|CommandTimeout = (INT32"60")|指定针对 SQL Server 执行查询时的命令超时（以秒为单位）。|
|**/p:**|DacApplicationDescription=(STRING)|定义要存储在 DACPAC 元数据中的应用程序说明。|
|**/p:**|DacApplicationName=(STRING)|定义要存储在 DACPAC 元数据中的应用程序名称。 默认值为数据库名称。|
|**/p:**|DacMajorVersion = (INT32"1")|定义要在 DACPAC 元数据中存储的主版本。|
|**/p:**|DacMinorVersion = (INT32 '0')|定义要在 DACPAC 元数据中存储的次版本。|
|**/p:**|ExtractAllTableData=(BOOLEAN)|指示是否提取所有用户表中的数据。 如果为 true，提取所有用户表中的数据，并不能指定单个用户表中提取数据的。 如果设置为 false，指定要从中提取数据的一个或多个用户表。|
|**/p:**|ExtractApplicationScopedObjectsOnly = (布尔值 True)|如果为 true，则只为指定的源提取应用程序范围的对象。 如果为 false，则为指定的源提取所有对象。|
|**/p:**|ExtractReferencedServerScopedElements = (布尔值 True)|如果为 true，则提取源数据库对象所引用的登录对象、服务器审核对象和凭据对象。|
|**/p:**|ExtractUsageProperties=(BOOLEAN)|指定了使用情况属性，例如表行数和索引大小，是否将从数据库中提取。|
|**/p:**|IgnoreExtendedProperties=(BOOLEAN)|指定是否应忽略扩展属性。|
|**/p:**|IgnorePermissions = (布尔值 True)|指定是否应忽略权限。|
|**/p:**|IgnoreUserLoginMappings=(BOOLEAN)|指定是否忽略用户和登录名之间的关系。|
|**/p:**|存储 = ({文件&#124;内存} File)|指定在提取过程中使用的架构模型的后备存储的类型。|
|**/p:**|TableData=(STRING)|指示将从中提取数据的表。 使用或不带括号住名称部分采用以下格式指定表名称： schema_name.table_identifier。|
|**/p:**|VerifyExtraction=(BOOLEAN)|指定是否应验证提取的 dacpac。|

## <a name="publish-parameters-properties-and-sqlcmd-variables"></a>发布参数、属性和 SQLCMD 变量

SqlPackage.exe 发布操作增量更新目标数据库的架构以便匹配源数据库的结构。 如果发布包含所有表或表子集的用户数据的部署包，则会更新架构和表数据。 数据部署覆盖目标数据库的现有表中的架构和数据。 对于未包含在部署包中的表，数据部署将不会更改目标数据库中的现有架构或数据。  

### <a name="help-for-publish-action"></a>有关发布操作的帮助

|参数|缩写|ReplTest1|描述|
|---|---|---|---|
|**/Action:**|**/a**|发布|指定要执行的操作。 |
|**/AccessToken:**|**/at**|{string}| 指定要在连接到目标数据库时使用的基于令牌的身份验证访问令牌。 |
|**/ AzureKeyVaultAuthMethod:**|**/akv**|{交互式&#124;ClientIdSecret}|指定用于访问 Azure Key Vault 的身份验证方法 |
|**/ClientId:**|**/cid**|{string}|必要时，指定在对 Azure KeyVault 进行身份验证时使用的客户端 ID |
|**/ DeployScriptPath:**|**/dsp**|{string}|指定要部署脚本输出的可选文件路径。 对于 Azure 部署，如果有用于创建或修改 master 数据库的 TSQL 命令，脚本便会写入相同路径，不同之处在于使用“Filename_Master.sql”作为输出文件名。 |
|**/ DeployReportPath:**|**/drp**|{string}|指定要部署报表的 xml 文件的输出的可选文件路径。 |
|**/Diagnostics:**|**/d**|{True&#124;False}|指定诊断日志记录是否输出到控制台。 默认为 False。 |
|**/ DiagnosticsFile:**|**/df**|{string}|指定一个用于存储诊断日志的文件。 |
|**/ MaxParallelism:**|**/mp**|{int}| 指定针对数据库运行的并发操作的并行度。 默认值为 8。 |
|**/ OverwriteFiles:**|**/of**|{True&#124;False}|指定 sqlpackage.exe 是否应覆盖现有文件。 指定 false 会导致 sqlpackage.exe 在遇到现有文件时中断操作。 默认值为 True。 |
|**/Profile:**|**/pr**|{string}|指定 DAC 发布配置文件的文件路径。 该配置文件定义在生成输出时要使用的属性和变量的集合。|
|**/Properties:**|**/p**|{PropertyName}={Value}|为特定于操作的属性指定名称值对；{PropertyName}={Value}。 请参考特定操作的帮助以便查看该操作的属性名称。 示例： sqlpackage.exe /Action： 发布 /？。|
|**/Quiet:**|**/q**|{True&#124;False}|指定是否隐藏详细反馈。 默认为 False。|
|**/Secret:**|**/secr**|{string}|必要时，指定在对 Azure KeyVault 进行身份验证时使用的客户端密码 |
|**/ SourceConnectionString:**|**/ scs**|{string}|指定源数据库的有效 SQL Server/Azure 连接字符串。 如果指定了此参数，则应该独立于所有其他源参数来使用此参数。 |
|**/SourceDatabaseName:**|**/sdn**|{string}|定义源数据库的名称。 |
|**/ SourceEncryptConnection:**|**/sec**|{True&#124;False}|指定是否应该将 SQL 加密用于源数据库连接。 |
|**/Sourcefile:**|**/sf**|{string}|指定要用作操作源而非数据库的源文件。 如果使用此参数，则其他源参数应无效。 |
|**/SourcePassword:**|**/sp**|{string}|对于 SQL Server 身份验证方案，定义要用于访问源数据库的密码。 |
|**/ SourceServerName:**|**/ssn**|{string}|定义承载源数据库的服务器的名称。 |
|**/ SourceTimeout:**|**/st**|{int}|指定建立与源数据库的连接的超时时间（以秒为单位）。 |
|**/ SourceTrustServerCertificate:**|**/stsc**|{True&#124;False}|指定是否使用 SSL 对源数据库连接进行加密并绕过证书链来验证信任。 |
|**/SourceUser:**|**/su**|{string}|对于 SQL Server 身份验证方案，定义要用于访问源数据库的 SQL Server 用户。 |
|**/ TargetConnectionString:**|**/tcs**|{string}|指定目标数据库的有效 SQL Server/Azure 连接字符串。 如果指定了此参数，则应该独立于所有其他目标参数来使用此参数。 |
|**/TargetDatabaseName:**|**/tdn**|{string}|指定作为 sqlpackage.exe 操作目标的数据库的替代名称。 |
|**/ TargetEncryptConnection:**|**/tec**|{True&#124;False}|指定是否应将 SQL 加密用于目标数据库连接。 |
|**/ TargetPassword:**|**/tp**|{string}|对于 SQL Server 身份验证方案，定义要用于访问目标数据库的密码。 |
|**/ TargetServerName:**|**/tsn**|{string}|定义承载目标数据库的服务器的名称。 |
|**/ TargetTimeout:**|**/tt**|{int}|指定建立与目标数据库的连接的超时时间（以秒为单位）。 对于 Azure AD，建议，此值是大于或等于 30 秒。|
|**/ TargetTrustServerCertificate:**|**/ttsc**|{True&#124;False}|指定是否使用 SSL 对目标数据库连接进行加密并绕过检查证书链来验证信任。 |
|**/ TargetUser:**|**/tu**|{string}|对于 SQL Server 身份验证方案，定义要用于访问目标数据库的 SQL Server 用户。 |
|**/TenantId:**|**/tid**|{string}|表示 Azure AD 租户 ID 或域名称。 此选项支持来宾所需或导入 Azure AD 用户，以及 Microsoft 帐户，如 outlook.com、 hotmail.com 或 live.com。 如果省略此参数，则将使用 Azure AD 的默认租户 ID，假定已经过身份验证的用户是此 AD 本机用户。 但是，在这种情况下任何来宾或导入的用户和/或在此 Azure AD 中托管的 Microsoft 帐户不支持，并且该操作将失败。 <br/> 有关 Active Directory 通用身份验证的详细信息，请参阅[SQL 数据库和 SQL 数据仓库 （对 MFA 的 SSMS 支持） 的通用身份验证](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)。|
|**/ UniversalAuthentication:**|**/ua**|{True&#124;False}|指定是否应使用通用身份验证。 设置为 True 时，支持 MFA 激活的交互式身份验证协议。 此选项还可用于 Azure AD 身份验证，而无需 MFA，使用交互式协议要求用户输入其用户名和密码或集成身份验证 （Windows 凭据）。 没有 Azure AD 身份验证时 /UniversalAuthentication 设置为 True，可以指定在 SourceConnectionString (/ scs)。 Azure AD 身份验证时 /UniversalAuthentication 设置为 False 时，必须指定在 SourceConnectionString (/ scs)。 <br/> 有关 Active Directory 通用身份验证的详细信息，请参阅[SQL 数据库和 SQL 数据仓库 （对 MFA 的 SSMS 支持） 的通用身份验证](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)。|
|**/Variables:**|**/v**|{PropertyName}={Value}|为特定于操作的变量指定名称值对；{VariableName}={Value}。 该 DACPAC 文件包含有效 SQLCMD 变量的列表。 如果没有为每个变量都提供值，则会发生错误。 |

### <a name="properties-specific-to-the-publish-action"></a>特定于发布操作的属性

|“属性”|ReplTest1|描述|
|---|---|---|
|**/p:**|AdditionalDeploymentContributorArguments=(STRING)|为部署参与者指定其他部署参与者参数。 这应该是用分号分隔的值列表。|
|**/p:**|AdditionalDeploymentContributors=(STRING)|指定应在部署 dacpac 时运行的其他部署参与者。 这应该是以分号分隔的完全限定的生成参与者名称或 ID 列表。|
|**/p:**|AllowDropBlockingAssemblies=(BOOLEAN)|SqlClr 部署使用此属性以导致阻塞程序集作为部署计划的组成部分被删除。 默认情况下，如果需要删除引用程序集，则任何阻塞或引用程序集将阻止程序集更新。|
|**/p:**|AllowIncompatiblePlatform=(BOOLEAN)|指定是否尝试操作，而不管存在的不兼容 SQL Server 平台。|
|**/p:**|AllowUnsafeRowLevelSecurityDataMovement=(BOOLEAN)|如果此属性设置为 true，则不阻止具有行级别安全性的表上的数据运动。 默认值为 false。|
|**/p:**|BackupDatabaseBeforeChanges=(BOOLEAN)|在部署任何更改之前，备份数据库。|
|**/p:**|BlockOnPossibleDataLoss = (布尔值 True)|指定在 publish.operation 可能导致数据丢失的情况下，应终止发布集。|
|**/p:**|BlockWhenDriftDetected = (布尔值 True)|指定是否阻止更新其架构与其注册不再匹配或已取消注册的数据库。|
|**/p:**|CommandTimeout = (INT32"60")|指定针对 SQL Server 执行查询时的命令超时（以秒为单位）。|
|**/p:**|CommentOutSetVarDeclarations=(BOOLEAN)|指定是否应在生成的发布脚本中注释掉 SETVAR 变量的声明。 如果您打算在发布时使用 SQLCMD.EXE 等工具指定命令行上的值，则可以选择这样做。|
|**/p:**|CompareUsingTargetCollation=(BOOLEAN)|此设置指示在部署过程中如何处理数据库的排序规则；默认情况下，如果目标数据库的排序规则与源所指定的排序规则不匹配，就将更新目标数据库的排序规则。 设置此选项后，应使用目标数据库（或服务器）的排序规则。|
|**/p:**|CreateNewDatabase=(BOOLEAN)|指定当您发布到数据库时，是否应更新目标数据库或是否应删除并重新创建目标数据库。|
|**/p:**|DatabaseEdition = ({Basic&#124;标准&#124;高级&#124;默认} Default)|定义版本的 Azure SQL 数据库。|
|**/p:**|DatabaseMaximumSize=(INT32)|定义 Azure SQL 数据库的大小上限（以 GB 为单位）。|
|**/p:**|DatabaseServiceObjective=(STRING)|定义 Azure SQL 数据库的性能级别，如“P0”或“S1”。|
|**/p:**|DeployDatabaseInSingleUserMode=(BOOLEAN)|如果为 true，则数据库在部署前将设置为单用户模式。|
|**/p:**|DisableAndReenableDdlTriggers = (布尔值 True)|指定在发布过程开始时是否禁用数据定义语言 (DDL) 触发器，以及在发布操作结束时是否重新启用此类触发器。|
|**/p:**|DoNotAlterChangeDataCaptureObjects = (布尔值 True)|如果为 true，则不更改变更数据捕获对象。|
|**/p:**|DoNotAlterReplicatedObjects = (布尔值 True)|指定是否在验证过程中标识重复的对象。|
|**/p:**|DoNotDropObjectType=(STRING)|当 DropObjectsNotInSource 为 true 时不应删除的对象类型。 有效的对象类型名称为 Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers。|
|**/p:**|DoNotDropObjectTypes=(STRING)|当 DropObjectsNotInSource 为 True 时不应删除的以分号分隔的对象类型列表。 有效的对象类型名称为 Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers。|
|**/p:**|DropConstraintsNotInSource = (布尔值 True)|指定当您发布到数据库时，是否将从目标数据库中删除数据库快照 (.dacpac) 文件中不存在的约束。|
|**/p:**|DropDmlTriggersNotInSource = (布尔值 True)|指定当您发布到数据库时，是否将从目标数据库中删除数据库快照 (.dacpac) 文件中不存在的 DML 触发器。|
|**/p:**|DropExtendedPropertiesNotInSource = (布尔值 True)|指定在发布到数据库时，是否将从目标数据库中删除数据库快照 (.dacpac) 文件中不存在的扩展属性。|
|**/p:**|DropIndexesNotInSource = (布尔值 True)|指定当您发布到数据库时，是否将从目标数据库中删除数据库快照 (.dacpac) 文件中不存在的索引。|
|**/p:**|DropObjectsNotInSource=(BOOLEAN)|指定当你发布到数据库时，是否将从目标数据库中删除数据库快照 (.dacpac) 文件中不存在的对象。 此值优先于 DropExtendedProperties。|
|**/p:**|DropPermissionsNotInSource=(BOOLEAN)|指定当您更新到数据库时，是否将从目标数据库中删除数据库快照 (.dacpac) 文件中不存在的权限。|
|**/p:**|DropRoleMembersNotInSource=(BOOLEAN)|指定当您更新到数据库时，是否将从目标数据库中删除数据库快照 (.dacpac) 文件中未定义的角色成员。|
|**/p:**|DropStatisticsNotInSource = (布尔值 True)|指定在发布到数据库时是否将从目标数据库中删除数据库快照 (.dacpac) 文件中不存在的统计信息。|
|**/p:**|ExcludeObjectType=(STRING)|应在部署期间忽略的对象类型。 有效的对象类型名称为 Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers。|
|**/p:**|ExcludeObjectTypes=(STRING)|在部署期间应忽略的以分号分隔的对象类型列表。 有效的对象类型名称为 Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers。|
|**/p:**|GenerateSmartDefaults=(BOOLEAN)|在使用一个不允许 Null 值的列更新一个包含数据的表时，自动提供默认值。|
|**/p:**|IgnoreAnsiNulls = (布尔值 True)|指定在发布到数据库时，是应忽略还是应更新 ANSI NULLS 设置方面的差异。|
|**/p:**|IgnoreAuthorizer=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新授权者方面的差异。|
|**/p:**|IgnoreColumnCollation=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新列排序规则方面的差异。|
|**/p:**|IgnoreColumnOrder=(BOOLEAN)|指定在发布到数据库时是否应忽略或更新表列顺序中的差异。|
|**/p:**|IgnoreComments=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新注释方面的差异。|
|**/p:**|IgnoreCryptographicProviderFilePath = (布尔值 True)|指定在发布到数据库时，是应忽略还是应更新加密提供程序的文件路径方面的差异。|
|**/p:**|IgnoreDdlTriggerOrder=(BOOLEAN)|指定在发布到数据库或服务器时，是应忽略还是更新数据定义语言 (DDL) 触发器中的顺序差异。|
|**/p:**|IgnoreDdlTriggerState=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新数据定义语言 (DDL) 触发器的启用状态或禁用状态方面的差异。|
|**/p:**|IgnoreDefaultSchema=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新默认架构方面的差异。|
|**/p:**|IgnoreDmlTriggerOrder=(BOOLEAN)|指定在发布到数据库时，是应忽略还是更新数据操作语言 (DML) 触发器中的顺序差异。|
|**/p:**|IgnoreDmlTriggerState=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新 DML 触发器的启用状态或禁用状态方面的差异。|
|**/p:**|IgnoreExtendedProperties=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新扩展属性方面的差异。|
|**/p:**|IgnoreFileAndLogFilePath = (布尔值 True)|指定在发布到数据库时，是应忽略还是应更新文件和日志文件路径方面的差异。|
|**/p:**|IgnoreFilegroupPlacement = (布尔值 True)|指定在发布到数据库时，是应忽略还是应更新 FILEGROUP 中的对象位置方面的差异。|
|**/p:**|IgnoreFileSize = (布尔值 True)|指定在发布到数据库时，是应忽略文件的大小差异，还是应发出警告。|
|**/p:**|IgnoreFillFactor = (布尔值 True)|指定在发布到数据库时，是应忽略索引存储的填充因子方面的差异，还是应发出警告。|
|**/p:**|IgnoreFullTextCatalogFilePath = (布尔值 True)|指定在发布到数据库时，是应忽略全文目录的文件路径方面的差异，还是应发出警告。|
|**/p:**|IgnoreIdentitySeed=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新标识列种子方面的差异。|
|**/p:**|IgnoreIncrement=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新标识列增量方面的差异。|
|**/p:**|IgnoreIndexOptions=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新索引选项方面的差异。|
|**/p:**|IgnoreIndexPadding = (布尔值 True)|指定在发布到数据库时，是应忽略还是应更新索引填充方面的差异。|
|**/p:**|IgnoreKeywordCasing = (布尔值 True)|指定在发布到数据库时，是应忽略还是应更新关键字的大小写方面的差异。|
|**/p:**|IgnoreLockHintsOnIndexes=(BOOLEAN)|指定当您发布到数据库时，应忽略还是更新索引上的锁提示之间的差异。|
|**/p:**|IgnoreLoginSids = (布尔值 True)|指定在发布到数据库时，是应忽略还是应更新安全标识号 (SID) 方面的差异。|
|**/p:**|IgnoreNotForReplication=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新不用于复制设置。|
|**/p:**|IgnoreObjectPlacementOnPartitionScheme = (布尔值 True)|指定在发布到数据库时，是应忽略还是应更新对象在分区方案中的位置。|
|**/p:**|IgnorePartitionSchemes=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新分区方案和分区函数方面的差异。|
|**/p:**|IgnorePermissions=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新权限方面的差异。|
|**/p:**|IgnoreQuotedIdentifiers = (布尔值 True)|指定在发布到数据库时，是应忽略还是应更新带引号的标识符设置方面的差异。|
|**/p:**|IgnoreRoleMembership=(BOOLEAN)|指定当您发布到数据库时，应忽略还是更新登录的角色成员身份之间的差异。|
|**/p:**|IgnoreRouteLifetime = (布尔值 True)|指定在发布到数据库时，应忽略还是应更新 SQL Server 保留路由表中的路由的时间量方面的差异。|
|**/p:**|IgnoreSemicolonBetweenStatements = (布尔值 True)|指定在发布到数据库时，是将忽略还是将更新 T-SQL 语句之间的分号差异。|
|**/p:**|IgnoreTableOptions=(BOOLEAN)|指定在发布到数据库时，是将忽略还是将更新表选项方面的差异。|
|**/p:**|IgnoreUserSettingsObjects=(BOOLEAN)|指定在发布到数据库时，是将忽略还是将更新用户设置对象方面的差异。|
|**/p:**|IgnoreWhitespace = (布尔值 True)|指定在发布到数据库时，是将忽略还是将更新空白方面的差异。|
|**/p:**|IgnoreWithNocheckOnCheckConstraints=(BOOLEAN)|指定在进行发布时，是将忽略还是将更新 CHECK 约束的 WITH NOCHECK 子句值方面的差异。|
|**/p:**|IgnoreWithNocheckOnForeignKeys=(BOOLEAN)|指定在发布到数据库时，是将忽略还是将更新外键的 WITH NOCHECK 子句值方面的差异。|
|**/p:**|IncludeCompositeObjects=(BOOLEAN)|将所有复合元素包含为单个发布操作的一部分。|
|**/p:**|IncludeTransactionalScripts=(BOOLEAN)|指定在发布到数据库时，是否应在可能的位置使用事务性语句。|
|**/p:**|NoAlterStatementsToChangeClrTypes=(BOOLEAN)|指定发布操作在存在差异时应始终删除并重新创建程序集，而不是发出 ALTER ASSEMBLY 语句。|
|**/p:**|PopulateFilesOnFileGroups = (布尔值 True)|指定当在目标数据库中创建新 FileGroup 时，是否也创建新文件。|
|**/p:**|RegisterDataTierApplication=(BOOLEAN)|指定是否向数据库服务器注册该架构。|
|**/p:**|RunDeploymentPlanExecutors=(BOOLEAN)|指定在执行其他操作时是否应运行 DeploymentPlanExecutor 参与者。|
|**/p:**|ScriptDatabaseCollation=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新数据库排序规则方面的差异。|
|**/p:**|ScriptDatabaseCompatibility=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新数据库兼容性方面的差异。|
|**/p:**|ScriptDatabaseOptions = (布尔值 True)|指定是否应作为发布操作的一部分来设置或更新目标数据库属性。|
|**/p:**|ScriptDeployStateChecks=(BOOLEAN)|指定是否在发布脚本中生成声明，以验证数据库名称和服务器名称是否与数据库项目中指定的名称匹配。|
|**/p:**|ScriptFileSize=(BOOLEAN)|控制在向文件组添加文件时是否指定大小。|
|**/p:**|ScriptNewConstraintValidation = (布尔值 True)|在发布的末尾的所有约束将被验证为一组，避免数据错误检查或外的键约束在发布过程引起的。 如果设置为“False”，则将发布约束而不检查对应的数据。|
|**/p:**|ScriptRefreshModule = (布尔值 True)|在发布脚本的末尾包括刷新语句。|
|**/p:**|存储 = ({文件&#124;内存})|指定在生成数据库模型时如何存储元素。 出于性能原因，默认值为 InMemory。 对于大型数据库，需要备份了文件的存储。|
|**/p:**|TreatVerificationErrorsAsWarnings=(BOOLEAN)|指定验证过程中遇到的错误发布是否应视为警告。 在对目标数据库执行生成的部署计划之前，会先对该计划执行检查。 计划验证将检测仅有目标的对象（如索引）丢失等问题，必须解决这些问题以进行更改。 验证还检测以下情况：依赖项（如表或视图）因对复合项目的引用而存在，但未存在于目标数据库中。 您可以选择执行此操作以获取所有问题，而不是让第一个出错时停止发布操作的完整列表。|**/p:**|UnmodifiableObjectWarnings = (布尔值 True)|指定在无法修改的对象中发现差异（例如，如果文件的大小或路径存在差异）时是否生成警告。|
|**/p:**|VerifyCollationCompatibility = (布尔值 True)|指定是否验证排序规则兼容性。|
|**/p:**|VerifyDeployment = (布尔值 True)|指定在出现可能阻止成功发布的问题的情况下，是否应在发布前执行将停止发布操作的检查。 例如，如果具有在数据库项目中不存在的目标数据库上的外键并且在发布时导致错误，则发布操作可能会停止。|
|

### <a name="sqlcmd-variables"></a>SQLCMD 变量

下表介绍可用于重写发布操作过程中使用的 SQL 命令 (sqlcmd) 变量的值的选项的格式。 命令行上指定的变量的值将重写分配给变量（例如，在发布配置文件中）的其他值。  
  
|参数|，则“默认”|描述|  
|-------------|-----------|---------------|  
|**/ 变量: {PropertyName} = {Value}**||为特定于操作的变量指定名称值对；{VariableName}={Value}。 该 DACPAC 文件包含有效 SQLCMD 变量的列表。 如果没有为每个变量都提供值，则会发生错误。|  
  
## <a name="export-parameters-and-properties"></a>导出参数和属性

SqlPackage.exe 导出操作将活动数据库从 SQL Server 或 Azure SQL 数据库导出到 BACPAC 包（.bacpac 文件）。 默认情况下，所有表的数据将包含在 .bacpac 文件中。 你可以选择仅指定要为其导出数据的表的子集。 即使针对导出指定表的子集，对导出操作的验证可确保 Azure SQL 数据库对完整目标数据库的兼容性。  
  
### <a name="help-for-export-action"></a>有关导出操作的帮助

|参数|缩写|ReplTest1|描述|
|---|---|---|---|
|**/Action:**|**/a**|导出|指定要执行的操作。 |
|**/AccessToken:**|**/at**|{string}| 指定要在连接到目标数据库时使用的基于令牌的身份验证访问令牌。 |
|**/Diagnostics:**|**/d**|{True&#124;False}|指定诊断日志记录是否输出到控制台。 默认为 False。 |
|**/ DiagnosticsFile:**|**/df**|{string}|指定一个用于存储诊断日志的文件。 |
|**/ MaxParallelism:**|**/mp**|{int}| 指定针对数据库运行的并发操作的并行度。 默认值为 8。 |
|**/ OverwriteFiles:**|**/of**|{True&#124;False}|指定 sqlpackage.exe 是否应覆盖现有文件。 指定 false 会导致 sqlpackage.exe 在遇到现有文件时中断操作。 默认值为 True。 |
|**/Properties:**|**/p**|{PropertyName}={Value}|为特定于操作的属性指定名称值对；{PropertyName}={Value}。 请参考特定操作的帮助以便查看该操作的属性名称。 示例： sqlpackage.exe /Action： 发布 /？。|
|**/Quiet:**|**/q**|{True&#124;False}|指定是否隐藏详细反馈。 默认为 False。|
|**/ SourceConnectionString:**|**/ scs**|{string}|指定源数据库的有效 SQL Server/Azure 连接字符串。 如果指定了此参数，则应该独立于所有其他源参数来使用此参数。 |
|**/SourceDatabaseName:**|**/sdn**|{string}|定义源数据库的名称。 |
|**/ SourceEncryptConnection:**|**/sec**|{True&#124;False}|指定是否应该将 SQL 加密用于源数据库连接。 |
|**/SourcePassword:**|**/sp**|{string}|对于 SQL Server 身份验证方案，定义要用于访问源数据库的密码。 |
|**/ SourceServerName:**|**/ssn**|{string}|定义承载源数据库的服务器的名称。 |
|**/ SourceTimeout:**|**/st**|{int}|指定建立与源数据库的连接的超时时间（以秒为单位）。 |
|**/ SourceTrustServerCertificate:**|**/stsc**|{True&#124;False}|指定是否使用 SSL 对源数据库连接进行加密并绕过证书链来验证信任。 |
|**/SourceUser:**|**/su**|{string}|对于 SQL Server 身份验证方案，定义要用于访问源数据库的 SQL Server 用户。 |
|**/TargetFile:**|**/tf**|{string}| 指定要用作操作而不是数据库的目标的目标文件 （即.dacpac 文件）。 如果使用此参数，则其他目标参数应无效。 此参数应仅支持数据库目标的操作无效。|
|**/TenantId:**|**/tid**|{string}|表示 Azure AD 租户 ID 或域名称。 此选项支持来宾所需或导入 Azure AD 用户，以及 Microsoft 帐户，如 outlook.com、 hotmail.com 或 live.com。 如果省略此参数，则将使用 Azure AD 的默认租户 ID，假定已经过身份验证的用户是此 AD 本机用户。 但是，在这种情况下任何来宾或导入的用户和/或在此 Azure AD 中托管的 Microsoft 帐户不支持，并且该操作将失败。 <br/> 有关 Active Directory 通用身份验证的详细信息，请参阅[SQL 数据库和 SQL 数据仓库 （对 MFA 的 SSMS 支持） 的通用身份验证](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)。|
|**/ UniversalAuthentication:**|**/ua**|{True&#124;False}|指定是否应使用通用身份验证。 设置为 True 时，支持 MFA 激活的交互式身份验证协议。 此选项还可用于 Azure AD 身份验证，而无需 MFA，使用交互式协议要求用户输入其用户名和密码或集成身份验证 （Windows 凭据）。 没有 Azure AD 身份验证时 /UniversalAuthentication 设置为 True，可以指定在 SourceConnectionString (/ scs)。 Azure AD 身份验证时 /UniversalAuthentication 设置为 False 时，必须指定在 SourceConnectionString (/ scs)。 <br/> 有关 Active Directory 通用身份验证的详细信息，请参阅[SQL 数据库和 SQL 数据仓库 （对 MFA 的 SSMS 支持） 的通用身份验证](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)。|

### <a name="properties-specific-to-the-export-action"></a>特定于导出操作的属性

|“属性”|ReplTest1|描述|
|---|---|---|
|**/p:**|CommandTimeout = (INT32"60")|指定针对 SQL Server 执行查询时的命令超时（以秒为单位）。|
|**/p:**|存储 = ({文件&#124;内存} File)|指定在提取过程中使用的架构模型的后备存储的类型。|
|**/p:**|TableData=(STRING)|指示将从中提取数据的表。 使用或不带括号住名称部分采用以下格式指定表名称： schema_name.table_identifier。|
|**/p:**|TargetEngineVersion = ({默认&#124;最新版本&#124;V11&#124;V12} 最新)|指定应使用的目标引擎版本。 这会影响是否允许具有 V12 功能，例如内存优化表，生成的 bacpac 中的 Azure SQL 数据库服务器所支持的对象。|
|**/p:**|VerifyFullTextDocumentTypesSupported=(BOOLEAN)|指定是否验证适用于 Microsoft Azure SQL 数据库 v12 的受支持全文文档类型。|
  
## <a name="import-parameters-and-properties"></a>导出参数和属性

SqlPackage.exe 导入操作将架构和表数据从 BACPAC 包（.bacpac 文件）导入到 SQL Server 或 Azure SQL 数据库中的新的或空白的数据库中。 在对现有数据库进行导入操作时，目标数据库无法包含任何用户定义的架构对象。  
  
### <a name="help-for-command-actions"></a>命令操作帮助

|参数|缩写|ReplTest1|描述|
|---|---|---|---|
|**/Action:**|**/a**|导入|指定要执行的操作。 |
|**/AccessToken:**|**/at**|{string}| 指定要在连接到目标数据库时使用的基于令牌的身份验证访问令牌。 |
|**/Diagnostics:**|**/d**|{True&#124;False}|指定诊断日志记录是否输出到控制台。 默认为 False。 |
|**/ DiagnosticsFile:**|**/df**|{string}|指定一个用于存储诊断日志的文件。 |
|**/ MaxParallelism:**|**/mp**|{int}| 指定针对数据库运行的并发操作的并行度。 默认值为 8。 |
|**/Properties:**|**/p**|{PropertyName}={Value}|为特定于操作的属性指定名称值对；{PropertyName}={Value}。 请参考特定操作的帮助以便查看该操作的属性名称。 示例： sqlpackage.exe /Action： 发布 /？。|
|**/Quiet:**|**/q**|{True&#124;False}|指定是否隐藏详细反馈。 默认为 False。|
|**/Sourcefile:**|**/sf**|{string}|指定要用作操作源的源文件。 如果使用此参数，则其他源参数应无效。 |
|**/ TargetConnectionString:**|**/tcs**|{string}|指定目标数据库的有效 SQL Server/Azure 连接字符串。 如果指定了此参数，则应该独立于所有其他目标参数来使用此参数。 |
|**/TargetDatabaseName:**|**/tdn**|{string}|指定作为 sqlpackage.exe 操作目标的数据库的替代名称。 |
|**/ TargetEncryptConnection:**|**/tec**|{True&#124;False}|指定是否应将 SQL 加密用于目标数据库连接。 |
|**/ TargetPassword:**|**/tp**|{string}|对于 SQL Server 身份验证方案，定义要用于访问目标数据库的密码。 |
|**/ TargetServerName:**|**/tsn**|{string}|定义承载目标数据库的服务器的名称。 |
|**/ TargetTimeout:**|**/tt**|{int}|指定建立与目标数据库的连接的超时时间（以秒为单位）。 对于 Azure AD，建议，此值是大于或等于 30 秒。|
|**/ TargetTrustServerCertificate:**|**/ttsc**|{True&#124;False}|指定是否使用 SSL 对目标数据库连接进行加密并绕过检查证书链来验证信任。 |
|**/ TargetUser:**|**/tu**|{string}|对于 SQL Server 身份验证方案，定义要用于访问目标数据库的 SQL Server 用户。 |
|**/TenantId:**|**/tid**|{string}|表示 Azure AD 租户 ID 或域名称。 此选项支持来宾所需或导入 Azure AD 用户，以及 Microsoft 帐户，如 outlook.com、 hotmail.com 或 live.com。 如果省略此参数，则将使用 Azure AD 的默认租户 ID，假定已经过身份验证的用户是此 AD 本机用户。 但是，在这种情况下任何来宾或导入的用户和/或在此 Azure AD 中托管的 Microsoft 帐户不支持，并且该操作将失败。 <br/> 有关 Active Directory 通用身份验证的详细信息，请参阅[SQL 数据库和 SQL 数据仓库 （对 MFA 的 SSMS 支持） 的通用身份验证](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)。|
|**/ UniversalAuthentication:**|**/ua**|{True&#124;False}|指定是否应使用通用身份验证。 设置为 True 时，支持 MFA 激活的交互式身份验证协议。 此选项还可用于 Azure AD 身份验证，而无需 MFA，使用交互式协议要求用户输入其用户名和密码或集成身份验证 （Windows 凭据）。 没有 Azure AD 身份验证时 /UniversalAuthentication 设置为 True，可以指定在 SourceConnectionString (/ scs)。 Azure AD 身份验证时 /UniversalAuthentication 设置为 False 时，必须指定在 SourceConnectionString (/ scs)。 <br/> 有关 Active Directory 通用身份验证的详细信息，请参阅[SQL 数据库和 SQL 数据仓库 （对 MFA 的 SSMS 支持） 的通用身份验证](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)。|

特定于导入操作的属性：
|“属性”|ReplTest1|描述|
|---|---|---|
|**/p:**|CommandTimeout = (INT32"60")|指定针对 SQL Server 执行查询时的命令超时（以秒为单位）。|
|**/p:**|DatabaseEdition = ({Basic&#124;标准&#124;高级&#124;默认} Default)|定义版本的 Azure SQL 数据库。|
|**/p:**|DatabaseMaximumSize=(INT32)|定义 Azure SQL 数据库的大小上限（以 GB 为单位）。|
|**/p:**|DatabaseServiceObjective=(STRING)|定义 Azure SQL 数据库的性能级别，如“P0”或“S1”。|
|**/p:**|ImportContributorArguments=(STRING)|为部署参与者指定部署参与者参数。 这应该是用分号分隔的值列表。|
|**/p:**|ImportContributors=(STRING)|指定导入 bacpac 时应运行的部署参与者。 这应该是以分号分隔的完全限定的生成参与者名称或 ID 列表。|
|**/p:**|存储 = ({文件&#124;内存})|指定在生成数据库模型时如何存储元素。 出于性能原因，默认值为 InMemory。 对于大型数据库，需要备份了文件的存储。|
  
## <a name="deployreport-parameters-and-properties"></a>DeployReport 参数和属性

SqlPackage.exe 报告操作创建将由发布操作完成的更改的 XML 报表。  
  
### <a name="help-for-deployreport-action"></a>DeployReport 操作的帮助

|参数|缩写|ReplTest1|描述|
|---|---|---|---|
|**/Action:**|**/a**|DeployReport|指定要执行的操作。 |
|**/AccessToken:**|**/at**|{string}| 指定要在连接到目标数据库时使用的基于令牌的身份验证访问令牌。 |
|**/Diagnostics:**|**/d**|{True&#124;False}|指定诊断日志记录是否输出到控制台。 默认为 False。 |
|**/ DiagnosticsFile:**|**/df**|{string}|指定一个用于存储诊断日志的文件。 |
|**/ MaxParallelism:**|**/mp**|{int}| 指定针对数据库运行的并发操作的并行度。 默认值为 8。 |
|**/OutputPath:**|**/op**|{string}|指定生成输出文件的文件路径。 |
|**/ OverwriteFiles:**|**/of**|{True&#124;False}|指定 sqlpackage.exe 是否应覆盖现有文件。 指定 false 会导致 sqlpackage.exe 在遇到现有文件时中断操作。 默认值为 True。 |
|**/Profile:**|**/pr**|{string}|指定 DAC 发布配置文件的文件路径。 该配置文件定义在生成输出时要使用的属性和变量的集合。 |
|**/Properties:**|**/p**|{PropertyName}={Value}|为特定于操作的属性指定名称值对；{PropertyName}={Value}。 请参考特定操作的帮助以便查看该操作的属性名称。 示例： sqlpackage.exe /Action： 发布 /？。 |
|**/Quiet:**|**/q**|{True&#124;False}|指定是否隐藏详细反馈。 默认为 False。 |
|**/ SourceConnectionString:**|**/ scs**|{string}|指定源数据库的有效 SQL Server/Azure 连接字符串。 如果指定了此参数，则应该独立于所有其他源参数来使用此参数。 |
|**/SourceDatabaseName:**|**/sdn**|{string}|定义源数据库的名称。 |
|**/ SourceEncryptConnection:**|**/sec**|{True&#124;False}|指定是否应该将 SQL 加密用于源数据库连接。 |
|**/Sourcefile:**|**/sf**|{string}|指定要用作操作源而非数据库的源文件。 如果使用此参数，则其他源参数应无效。 |
|**/SourcePassword:**|**/sp**|{string}|对于 SQL Server 身份验证方案，定义要用于访问源数据库的密码。 |
|**/ SourceServerName:**|**/ssn**|{string}|定义承载源数据库的服务器的名称。 |
|**/ SourceTimeout:**|**/st**|{int}|指定建立与源数据库的连接的超时时间（以秒为单位）。 |
|**/ SourceTrustServerCertificate:**|**/stsc**|{True&#124;False}|指定是否使用 SSL 对源数据库连接进行加密并绕过证书链来验证信任。 |
|**/SourceUser:**|**/su**|{string}|对于 SQL Server 身份验证方案，定义要用于访问源数据库的 SQL Server 用户。 |
|**/ TargetConnectionString:**|**/tcs**|{string}|指定目标数据库的有效 SQL Server/Azure 连接字符串。 如果指定了此参数，则应该独立于所有其他目标参数来使用此参数。 |
|**/TargetDatabaseName:**|**/tdn**|{string}|指定作为 sqlpackage.exe 操作目标的数据库的替代名称。 |
|**/ TargetEncryptConnection:**|**/tec**|{True&#124;False}|指定是否应将 SQL 加密用于目标数据库连接。 |
|**/TargetFile:**|**/tf**|{string}|指定要用作操作而不是数据库的目标的目标文件 （即.dacpac 文件）。 如果使用此参数，则其他目标参数应无效。 此参数应仅支持数据库目标的操作无效。|
|**/ TargetPassword:**|**/tp**|{string}|对于 SQL Server 身份验证方案，定义要用于访问目标数据库的密码。 |
|**/ TargetServerName:**|**/tsn**|{string}|定义承载目标数据库的服务器的名称。 |
|**/ TargetTimeout:**|**/tt**|{int}|指定建立与目标数据库的连接的超时时间（以秒为单位）。 对于 Azure AD，建议，此值是大于或等于 30 秒。|
|**/ TargetTrustServerCertificate:**|**/ttsc**|{True&#124;False}|指定是否使用 SSL 对目标数据库连接进行加密并绕过检查证书链来验证信任。 |
|**/ TargetUser:**|**/tu**|{string}|对于 SQL Server 身份验证方案，定义要用于访问目标数据库的 SQL Server 用户。 |
|**/TenantId:**|**/tid**|{string}|表示 Azure AD 租户 ID 或域名称。 此选项支持来宾所需或导入 Azure AD 用户，以及 Microsoft 帐户，如 outlook.com、 hotmail.com 或 live.com。 如果省略此参数，则将使用 Azure AD 的默认租户 ID，假定已经过身份验证的用户是此 AD 本机用户。 但是，在这种情况下任何来宾或导入的用户和/或在此 Azure AD 中托管的 Microsoft 帐户不支持，并且该操作将失败。 <br/> 有关 Active Directory 通用身份验证的详细信息，请参阅[SQL 数据库和 SQL 数据仓库 （对 MFA 的 SSMS 支持） 的通用身份验证](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)。|
|**/ UniversalAuthentication:**|**/ua**|{True&#124;False}|指定是否应使用通用身份验证。 设置为 True 时，支持 MFA 激活的交互式身份验证协议。 此选项还可用于 Azure AD 身份验证，而无需 MFA，使用交互式协议要求用户输入其用户名和密码或集成身份验证 （Windows 凭据）。 没有 Azure AD 身份验证时 /UniversalAuthentication 设置为 True，可以指定在 SourceConnectionString (/ scs)。 Azure AD 身份验证时 /UniversalAuthentication 设置为 False 时，必须指定在 SourceConnectionString (/ scs)。 <br/> 有关 Active Directory 通用身份验证的详细信息，请参阅[SQL 数据库和 SQL 数据仓库 （对 MFA 的 SSMS 支持） 的通用身份验证](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)。|
|**/Variables:**|**/v**|{PropertyName}={Value}|为特定于操作的变量指定名称值对；{VariableName}={Value}。 该 DACPAC 文件包含有效 SQLCMD 变量的列表。 如果没有为每个变量都提供值，则会发生错误。 |

## <a name="properties-specific-to-the-deployreport-action"></a>特定于 DeployReport 操作属性

|“属性”|ReplTest1|描述|
|---|---|---|
|**/p:**|AdditionalDeploymentContributorArguments=(STRING)|为部署参与者指定其他部署参与者参数。 这应该是用分号分隔的值列表。|
|**/p:**|AdditionalDeploymentContributors=(STRING)|指定应在部署 dacpac 时运行的其他部署参与者。 这应该是以分号分隔的完全限定的生成参与者名称或 ID 列表。|
|**/p:**|AllowDropBlocking Assemblies=(BOOLEAN)|SqlClr 部署使用此属性以导致阻塞程序集作为部署计划的组成部分被删除。 默认情况下，如果需要删除引用程序集，则任何阻塞或引用程序集将阻止程序集更新。|
|**/p:**|AllowIncompatiblePlatform=(BOOLEAN)|指定是否尝试操作，而不管存在的不兼容 SQL Server 平台。|
|**/p:**|AllowUnsafeRowLevelSecurityDataMovement=(BOOLEAN)|如果此属性设置为 true，则不阻止具有行级别安全性的表上的数据运动。 默认值为 false。|
|**/p:**|BackupDatabaseBeforeChanges=(BOOLEAN)|在部署任何更改之前，备份数据库。|
|**/p:**|BlockOnPossibleDataLoss = (布尔值 True)|指定在 publish.operation 可能导致数据丢失的情况下，应终止发布集。|
|**/p:**|BlockWhenDriftDetected = (布尔值 True)|指定是否阻止更新其架构与其注册不再匹配或已取消注册的数据库。 |
|**/p:**|CommandTimeout = (INT32"60")|指定针对 SQL Server 执行查询时的命令超时（以秒为单位）。 |
|**/p:**|CommentOutSetVarDeclarations=(BOOLEAN)|指定是否应在生成的发布脚本中注释掉 SETVAR 变量的声明。 如果您打算在发布时使用 SQLCMD.EXE 等工具指定命令行上的值，则可以选择这样做。 |
|**/p:**|CompareUsingTargetCollation=(BOOLEAN)|此设置指示在部署过程中如何处理数据库的排序规则；默认情况下，如果目标数据库的排序规则与源所指定的排序规则不匹配，就将更新目标数据库的排序规则。 设置此选项后，应使用目标数据库（或服务器）的排序规则。 |
|**/p:**|CreateNewDatabase=(BOOLEAN)|指定当您发布到数据库时，是否应更新目标数据库或是否应删除并重新创建目标数据库。 |
|**/p:**|DatabaseEdition = ({Basic&#124;标准&#124;高级&#124;默认} Default)|定义版本的 Azure SQL 数据库。 |
|**/p:**|DatabaseMaximumSize=(INT32)|定义 Azure SQL 数据库的大小上限（以 GB 为单位）。|
|**/p:**|DatabaseServiceObjective=(STRING)|定义 Azure SQL 数据库的性能级别，如“P0”或“S1”。 |
|**/p:**|DeployDatabaseInSingleUserMode=(BOOLEAN)|如果为 true，则数据库在部署前将设置为单用户模式。 |
|**/p:**|DisableAndReenableDdlTriggers = (布尔值 True)| 指定在发布过程开始时是否禁用数据定义语言 (DDL) 触发器，以及在发布操作结束时是否重新启用此类触发器。|
|**/p:**|DoNotAlterChangeDataCaptureObjects = (布尔值 True)|如果为 true，则不更改变更数据捕获对象。|
|**/p:**|DoNotAlterReplicatedObjects = (布尔值 True)|指定是否在验证过程中标识重复的对象。|
|**/p:**|DoNotDropObjectType=(STRING)|当 DropObjectsNotInSource 为 true 时不应删除的对象类型。 有效的对象类型名称为 Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers。 |
|**/p:**|DoNotDropObjectTypes=(STRING)|当 DropObjectsNotInSource 为 True 时不应删除的以分号分隔的对象类型列表。 有效的对象类型名称为 Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers。|
|**/p:**|DropConstraintsNotInSource = (布尔值 True)|指定当您发布到数据库时，是否将从目标数据库中删除数据库快照 (.dacpac) 文件中不存在的约束。|
|**/p:**|DropDmlTriggersNotInSource = (布尔值 True)|指定当您发布到数据库时，是否将从目标数据库中删除数据库快照 (.dacpac) 文件中不存在的 DML 触发器。|
|**/p:**|DropExtendedPropertiesNotInSource = (布尔值 True)|指定在发布到数据库时，是否将从目标数据库中删除数据库快照 (.dacpac) 文件中不存在的扩展属性。|
|**/p:**|DropIndexesNotInSource = (布尔值 True)|指定当您发布到数据库时，是否将从目标数据库中删除数据库快照 (.dacpac) 文件中不存在的索引。|
|**/p:**|DropObjectsNotInSource=(BOOLEAN)|指定当你发布到数据库时，是否将从目标数据库中删除数据库快照 (.dacpac) 文件中不存在的对象。 此值优先于 DropExtendedProperties。|
|**/p:**|DropPermissionsNotInSource=(BOOLEAN)|指定当您更新到数据库时，是否将从目标数据库中删除数据库快照 (.dacpac) 文件中不存在的权限。|
|**/p:**|DropRoleMembersNotInSource=(BOOLEAN)|指定当您更新到数据库时，是否将从目标数据库中删除数据库快照 (.dacpac) 文件中未定义的角色成员。|
|**/p:**|DropStatisticsNotInSource = (布尔值 True)|指定在发布到数据库时是否将从目标数据库中删除数据库快照 (.dacpac) 文件中不存在的统计信息。|
|**/p:**|ExcludeObjectType=(STRING)|应在部署期间忽略的对象类型。 有效的对象类型名称为 Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers。|
|**/p:**|ExcludeObjectTypes=(STRING)|在部署期间应忽略的以分号分隔的对象类型列表。 有效的对象类型名称为 Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers。|
|**/p:**|GenerateSmartDefaults=(BOOLEAN)|在使用一个不允许 Null 值的列更新一个包含数据的表时，自动提供默认值。|
|**/p:**|IgnoreAnsiNulls = (布尔值 True)|指定在发布到数据库时，是应忽略还是应更新 ANSI NULLS 设置方面的差异。|
|**/p:**|IgnoreAuthorizer=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新授权者方面的差异。|
|**/p:**|IgnoreColumnCollation=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新列排序规则方面的差异。|
|**/p:**|IgnoreColumnOrder=(BOOLEAN)|指定在发布到数据库时是否应忽略或更新表列顺序中的差异。|
|**/p:**|IgnoreComments=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新注释方面的差异。|
|**/p:**|IgnoreCryptographicProviderFilePath = (布尔值 True)|指定在发布到数据库时，是应忽略还是应更新加密提供程序的文件路径方面的差异。|
|**/p:**|IgnoreDdlTriggerOrder=(BOOLEAN)|指定在发布到数据库或服务器时，是应忽略还是更新数据定义语言 (DDL) 触发器中的顺序差异。|
|**/p:**|IgnoreDdlTriggerState=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新数据定义语言 (DDL) 触发器的启用状态或禁用状态方面的差异。|
|**/p:**|IgnoreDefaultSchema=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新默认架构方面的差异。 |
|**/p:**|IgnoreDmlTriggerOrder=(BOOLEAN)|指定在发布到数据库时，是应忽略还是更新数据操作语言 (DML) 触发器中的顺序差异。| 
|**/p:**|IgnoreDmlTriggerState=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新 DML 触发器的启用状态或禁用状态方面的差异。 |
|**/p:**|IgnoreExtendedProperties=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新扩展属性方面的差异。 |
|**/p:**|IgnoreFileAndLogFilePath = (布尔值 True)|指定在发布到数据库时，是应忽略还是应更新文件和日志文件路径方面的差异。 |
|**/p:**|IgnoreFilegroupPlacement = (布尔值 True)|指定在发布到数据库时，是应忽略还是应更新 FILEGROUP 中的对象位置方面的差异。| 
|**/p:**|IgnoreFileSize = (布尔值 True)|指定在发布到数据库时，是应忽略文件的大小差异，还是应发出警告。 |
|**/p:**|IgnoreFillFactor = (布尔值 True)|指定在发布到数据库时，是应忽略索引存储的填充因子方面的差异，还是应发出警告|
|**/p:**|IgnoreFullTextCatalogFilePath = (布尔值 True)|指定在发布到数据库时，是应忽略全文目录的文件路径方面的差异，还是应发出警告。| 
|**/p:**|IgnoreIdentitySeed=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新标识列种子方面的差异。 |
|**/p:**|IgnoreIncrement=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新标识列增量方面的差异。 |
|**/p:**|IgnoreIndexOptions=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新索引选项方面的差异。 |
|**/p:**|IgnoreIndexPadding = (布尔值 True)|指定在发布到数据库时，是应忽略还是应更新索引填充方面的差异。 |
|**/p:**|IgnoreKeywordCasing = (布尔值 True)|指定在发布到数据库时，是应忽略还是应更新关键字的大小写方面的差异。 |
|**/p:**|IgnoreLockHintsOnIndexes=(BOOLEAN)|指定当您发布到数据库时，应忽略还是更新索引上的锁提示之间的差异。 |
|**/p:**|IgnoreLoginSids = (布尔值 True)| 指定在发布到数据库时，是应忽略还是应更新安全标识号 (SID) 方面的差异。| 
|**/p:**|IgnoreNotForReplication=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新不用于复制设置。 |
|**/p:**|IgnoreObjectPlacementOnPartitionScheme = (布尔值 True)|指定在发布到数据库时，是应忽略还是应更新对象在分区方案中的位置。|
 |**/p:**|IgnorePartitionSchemes=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新分区方案和分区函数方面的差异。|
|**/p:**|IgnorePermissions=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新权限方面的差异。 |
|**/p:**|IgnoreQuotedIdentifiers = (布尔值 True)|指定在发布到数据库时，是应忽略还是应更新带引号的标识符设置方面的差异。 |
|**/p:**|IgnoreRoleMembership=(BOOLEAN)|指定当您发布到数据库时，应忽略还是更新登录的角色成员身份之间的差异。 |
|**/p:**|IgnoreRouteLifetime = (布尔值 True)|指定在发布到数据库时，是应忽略还是应更新 SQL Server 保留路由表中的路由的时间量方面的差异|
|**/p:**|IgnoreSemicolonBetweenStatements = (布尔值 True)|指定在发布到数据库时，是将忽略还是将更新 T-SQL 语句之间的分号差异。| 
|**/p:**|IgnoreTableOptions=(BOOLEAN)|指定在发布到数据库时，是将忽略还是将更新表选项方面的差异。| 
|**/p:**|IgnoreUserSettingsObjects=(BOOLEAN)|指定在发布到数据库时，是将忽略还是将更新用户设置对象方面的差异。|
|**/p:**|IgnoreWhitespace = (布尔值 True)|指定在发布到数据库时，是将忽略还是将更新空白方面的差异。 |
|**/p:**|IgnoreWithNocheckOnCheckConstraints=(BOOLEAN)|指定在发布到数据库时，是将忽略还是将更新 CHECK 约束的 WITH NOCHECK 子句值方面的差异。| 
|**/p:**|IgnoreWithNocheckOnForeignKeys=(BOOLEAN)|指定在发布到数据库时，是将忽略还是将更新外键的 WITH NOCHECK 子句值方面的差异。| 
|**/p:**|IncludeCompositeObjects=(BOOLEAN)|将所有复合元素包含为单个发布操作的一部分。|
|**/p:**|IncludeTransactionalScripts=(BOOLEAN)|指定在发布到数据库时，是否应在可能的位置使用事务性语句。|
 |**/p:**|NoAlterStatementsToChangeClrTypes=(BOOLEAN)|指定发布操作在存在差异时应始终删除并重新创建程序集，而不是发出 ALTER ASSEMBLY 语句。 |
|**/p:**|PopulateFilesOnFileGroups = (布尔值 True)|指定当在目标数据库中创建新 FileGroup 时，是否也创建新文件。 |
|**/p:**|RegisterDataTierApplication=(BOOLEAN)|指定是否向数据库服务器注册该架构。 
|**/p:**|RunDeploymentPlanExecutors=(BOOLEAN)|指定在执行其他操作时是否应运行 DeploymentPlanExecutor 参与者。|
|**/p:**|ScriptDatabaseCollation=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新数据库排序规则方面的差异。 |
|**/p:**|ScriptDatabaseCompatibility=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新数据库兼容性方面的差异。 |
|**/p:**|ScriptDatabaseOptions = (布尔值 True)|指定是否应作为发布操作的一部分来设置或更新目标数据库属性。 |
|**/p:**|ScriptDeployStateChecks=(BOOLEAN)|指定是否在发布脚本中生成声明，以验证数据库名称和服务器名称是否与数据库项目中指定的名称匹配。|
|**/p:**|ScriptFileSize=(BOOLEAN)|控制在向文件组添加文件时是否指定大小。 |
|**/p:**|ScriptNewConstraintValidation = (布尔值 True)|在发布的末尾的所有约束将被验证为一组，避免数据错误检查或外的键约束在发布过程引起的。 如果设置为“False”，则将发布约束而不检查对应的数据。|
|**/p:**|ScriptRefreshModule = (布尔值 True)|在发布脚本的末尾包括刷新语句。|
|**/p:**|存储 = ({文件&#124;内存})|指定在生成数据库模型时如何存储元素。 出于性能原因，默认值为 InMemory。 对于大型数据库，需要备份了文件的存储。|
|**/p:**|TreatVerificationErrorsAsWarnings=(BOOLEAN)|指定验证过程中遇到的错误发布是否应视为警告。 在对目标数据库执行生成的部署计划之前，会先对该计划执行检查。 计划验证将检测仅有目标的对象（如索引）丢失等问题，必须解决这些问题以进行更改。 验证还检测以下情况：依赖项（如表或视图）因对复合项目的引用而存在，但未存在于目标数据库中。 您可以选择执行此操作以获取所有问题，而不是让第一个出错时停止发布操作的完整列表。 |
|**/p:**|UnmodifiableObjectWarnings = (布尔值 True)|指定在无法修改的对象中发现差异（例如，如果文件的大小或路径存在差异）时是否生成警告。| 
|**/p:**|VerifyCollationCompatibility = (布尔值 True)|指定是否验证排序规则兼容性。| 
|**/p:**|VerifyDeployment = (布尔值 True)|指定在出现可能阻止成功发布的问题的情况下，是否应在发布前执行将停止发布操作的检查。 例如，如果具有在数据库项目中不存在的目标数据库上的外键并且在发布时导致错误，则发布操作可能会停止。 |
  
## <a name="driftreport-parameters"></a>DriftReport 参数

SqlPackage.exe 报告操作创建自注册数据库注册以来已对其做出的更改的 XML 报表。  
  
### <a name="help-for-driftreport-action"></a>DriftReport 操作有关的帮助

|参数|缩写|ReplTest1|描述|
|---|---|---|---|
|**/Action:**|**/a**|DriftReport|指定要执行的操作。 |
|**/AccessToken:**|**/at**|{string}| 指定要在连接到目标数据库时使用的基于令牌的身份验证访问令牌。 |
|**/Diagnostics:**|**/d**|{True&#124;False}|指定诊断日志记录是否输出到控制台。 默认为 False。 |
|**/ DiagnosticsFile:**|**/df**|{string}|指定一个用于存储诊断日志的文件。 |
|**/ MaxParallelism:**|**/mp**|{int}| 指定针对数据库运行的并发操作的并行度。 默认值为 8。 |
|**/OutputPath:**|**/op**|{string}|指定生成输出文件的文件路径。 |
|**/ OverwriteFiles:**|**/of**|{True&#124;False}|指定 sqlpackage.exe 是否应覆盖现有文件。 指定 false 会导致 sqlpackage.exe 在遇到现有文件时中断操作。 默认值为 True。 |
|**/Quiet:**|**/q**|{True&#124;False}|指定是否隐藏详细反馈。 默认为 False。|
|**/ TargetConnectionString:**|**/tcs**|{string}|指定目标数据库的有效 SQL Server/Azure 连接字符串。 如果指定了此参数，则应该独立于所有其他目标参数来使用此参数。 |
|**/TargetDatabaseName:**|**/tdn**|{string}|指定作为 sqlpackage.exe 操作目标的数据库的替代名称。 |
|**/ TargetEncryptConnection:**|**/tec**|{True&#124;False}|指定是否应将 SQL 加密用于目标数据库连接。 |
|**/ TargetPassword:**|**/tp**|{string}|对于 SQL Server 身份验证方案，定义要用于访问目标数据库的密码。 |
|**/ TargetServerName:**|**/tsn**|{string}|定义承载目标数据库的服务器的名称。 |
|**/ TargetTimeout:**|**/tt**|{int}|指定建立与目标数据库的连接的超时时间（以秒为单位）。 对于 Azure AD，建议，此值是大于或等于 30 秒。|
|**/ TargetTrustServerCertificate:**|**/ttsc**|{True&#124;False}|指定是否使用 SSL 对目标数据库连接进行加密并绕过检查证书链来验证信任。 |
|**/ TargetUser:**|**/tu**|{string}|对于 SQL Server 身份验证方案，定义要用于访问目标数据库的 SQL Server 用户。 |
|**/TenantId:**|**/tid**|{string}|表示 Azure AD 租户 ID 或域名称。 此选项支持来宾所需或导入 Azure AD 用户，以及 Microsoft 帐户，如 outlook.com、 hotmail.com 或 live.com。 如果省略此参数，则将使用 Azure AD 的默认租户 ID，假定已经过身份验证的用户是此 AD 本机用户。 但是，在这种情况下任何来宾或导入的用户和/或在此 Azure AD 中托管的 Microsoft 帐户不支持，并且该操作将失败。 <br/> 有关 Active Directory 通用身份验证的详细信息，请参阅[SQL 数据库和 SQL 数据仓库 （对 MFA 的 SSMS 支持） 的通用身份验证](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)。|
|**/ UniversalAuthentication:**|**/ua**|{True&#124;False}|指定是否应使用通用身份验证。 设置为 True 时，支持 MFA 激活的交互式身份验证协议。 此选项还可用于 Azure AD 身份验证，而无需 MFA，使用交互式协议要求用户输入其用户名和密码或集成身份验证 （Windows 凭据）。 没有 Azure AD 身份验证时 /UniversalAuthentication 设置为 True，可以指定在 SourceConnectionString (/ scs)。 Azure AD 身份验证时 /UniversalAuthentication 设置为 False 时，必须指定在 SourceConnectionString (/ scs)。 <br/> 有关 Active Directory 通用身份验证的详细信息，请参阅[SQL 数据库和 SQL 数据仓库 （对 MFA 的 SSMS 支持） 的通用身份验证](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)。|

## <a name="script-parameters-and-properties"></a>脚本参数和属性

SqlPackage.exe 脚本操作会创建 Transact-SQL 增量更新脚本，该脚本可更新目标数据库的架构以匹配源数据库的架构。  
  
### <a name="help-for-the-script-action"></a>有关脚本操作的帮助

|参数|缩写|ReplTest1|描述|
|---|---|---|---|
|**/Action:**|**/a**|脚本|指定要执行的操作。 |
|**/AccessToken:**|**/at**|{string}| 指定要在连接到目标数据库时使用的基于令牌的身份验证访问令牌。 |
|**/ DeployScriptPath:**|**/dsp**|{string}|指定要部署脚本输出的可选文件路径。 对于 Azure 部署，如果有用于创建或修改 master 数据库的 TSQL 命令，脚本便会写入相同路径，不同之处在于使用“Filename_Master.sql”作为输出文件名。 |
|**/ DeployReportPath:**|**/drp**|{string}|指定要部署报表的 xml 文件的输出的可选文件路径。 |
|**/Diagnostics:**|**/d**|{True&#124;False}|指定诊断日志记录是否输出到控制台。 默认为 False。 |
|**/ DiagnosticsFile:**|**/df**|{string}|指定一个用于存储诊断日志的文件。 |
|**/ MaxParallelism:**|**/mp**|{int}| 指定针对数据库运行的并发操作的并行度。 默认值为 8。 |
|**/OutputPath:**|**/op**|{string}|指定生成输出文件的文件路径。 |
|**/ OverwriteFiles:**|**/of**|{True&#124;False}|指定 sqlpackage.exe 是否应覆盖现有文件。 指定 false 会导致 sqlpackage.exe 在遇到现有文件时中断操作。 默认值为 True。 |
|**/Profile:**|**/pr**|{string}|指定 DAC 发布配置文件的文件路径。 该配置文件定义在生成输出时要使用的属性和变量的集合。|
|**/Properties:**|**/p**|{PropertyName}={Value}|为特定于操作的属性指定名称值对；{PropertyName}={Value}。 请参考特定操作的帮助以便查看该操作的属性名称。 示例： sqlpackage.exe /Action： 发布 /？。|
|**/Quiet:**|**/q**|{True&#124;False}|指定是否隐藏详细反馈。 默认为 False。|
|**/ SourceConnectionString:**|**/ scs**|{string}|指定源数据库的有效 SQL Server/Azure 连接字符串。 如果指定了此参数，则应该独立于所有其他源参数来使用此参数。 |
|**/SourceDatabaseName:**|**/sdn**|{string}|定义源数据库的名称。 |
|**/ SourceEncryptConnection:**|**/sec**|{True&#124;False}|指定是否应该将 SQL 加密用于源数据库连接。 |
|**/Sourcefile:**|**/sf**|{string}|指定要用作操作源的源文件。 如果使用此参数，则其他源参数应无效。 |
|**/SourcePassword:**|**/sp**|{string}|对于 SQL Server 身份验证方案，定义要用于访问源数据库的密码。 |
|**/ SourceServerName:**|**/ssn**|{string}|定义承载源数据库的服务器的名称。 |
|**/ SourceTimeout:**|**/st**|{int}|指定建立与源数据库的连接的超时时间（以秒为单位）。 |
|**/ SourceTrustServerCertificate:**|**/stsc**|{True&#124;False}|指定是否使用 SSL 对源数据库连接进行加密并绕过证书链来验证信任。 |
|**/SourceUser:**|**/su**|{string}|对于 SQL Server 身份验证方案，定义要用于访问源数据库的 SQL Server 用户。 |
|**/ TargetConnectionString:**|**/tcs**|{string}|指定目标数据库的有效 SQL Server/Azure 连接字符串。 如果指定了此参数，则应该独立于所有其他目标参数来使用此参数。 |
|**/TargetDatabaseName:**|**/tdn**|{string}|指定作为 sqlpackage.exe 操作目标的数据库的替代名称。 |
|**/ TargetEncryptConnection:**|**/tec**|{True&#124;False}|指定是否应将 SQL 加密用于目标数据库连接。 |
|**/TargetFile:**|**/tf**|{string}| 指定要用作操作而不是数据库的目标的目标文件 （即.dacpac 文件）。 如果使用此参数，则其他目标参数应无效。 此参数应仅支持数据库目标的操作无效。|
|**/ TargetPassword:**|**/tp**|{string}|对于 SQL Server 身份验证方案，定义要用于访问目标数据库的密码。 |
|**/ TargetServerName:**|**/tsn**|{string}|定义承载目标数据库的服务器的名称。 |
|**/ TargetTimeout:**|**/tt**|{int}|指定建立与目标数据库的连接的超时时间（以秒为单位）。 对于 Azure AD，建议，此值是大于或等于 30 秒。|
|**/ TargetTrustServerCertificate:**|**/ttsc**|{True&#124;False}|指定是否使用 SSL 对目标数据库连接进行加密并绕过检查证书链来验证信任。 |
|**/ TargetUser:**|**/tu**|{string}|对于 SQL Server 身份验证方案，定义要用于访问目标数据库的 SQL Server 用户。 |
|**/TenantId:**|**/tid**|{string}|表示 Azure AD 租户 ID 或域名称。 此选项支持来宾所需或导入 Azure AD 用户，以及 Microsoft 帐户，如 outlook.com、 hotmail.com 或 live.com。 如果省略此参数，则将使用 Azure AD 的默认租户 ID，假定已经过身份验证的用户是此 AD 本机用户。 但是，在这种情况下任何来宾或导入的用户和/或在此 Azure AD 中托管的 Microsoft 帐户不支持，并且该操作将失败。 <br/> 有关 Active Directory 通用身份验证的详细信息，请参阅[SQL 数据库和 SQL 数据仓库 （对 MFA 的 SSMS 支持） 的通用身份验证](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)。|
|**/ UniversalAuthentication:**|**/ua**|{True&#124;False}|指定是否应使用通用身份验证。 设置为 True 时，支持 MFA 激活的交互式身份验证协议。 此选项还可用于 Azure AD 身份验证，而无需 MFA，使用交互式协议要求用户输入其用户名和密码或集成身份验证 （Windows 凭据）。 没有 Azure AD 身份验证时 /UniversalAuthentication 设置为 True，可以指定在 SourceConnectionString (/ scs)。 Azure AD 身份验证时 /UniversalAuthentication 设置为 False 时，必须指定在 SourceConnectionString (/ scs)。 <br/> 有关 Active Directory 通用身份验证的详细信息，请参阅[SQL 数据库和 SQL 数据仓库 （对 MFA 的 SSMS 支持） 的通用身份验证](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)。|
|**/Variables:**|**/v**|{PropertyName}={Value}|为特定于操作的变量指定名称值对；{VariableName}={Value}。 该 DACPAC 文件包含有效 SQLCMD 变量的列表。 如果没有为每个变量都提供值，则会发生错误。 |

### <a name="properties-specific-to-the-script-action"></a>特定于脚本操作属性

|“属性”|ReplTest1|描述|
|---|---|---|
|**/p:**|AdditionalDeploymentContributorArguments=(STRING)|为部署参与者指定其他部署参与者参数。 这应该是用分号分隔的值列表。
|**/p:**|AdditionalDeploymentContributors=(STRING)|指定应在部署 dacpac 时运行的其他部署参与者。 这应该是以分号分隔的完全限定的生成参与者名称或 ID 列表。
|**/p:**|AllowDropBlockingAssemblies=(BOOLEAN)|SqlClr 部署使用此属性以导致阻塞程序集作为部署计划的组成部分被删除。 默认情况下，如果需要删除引用程序集，则任何阻塞或引用程序集将阻止程序集更新。
|**/p:**|AllowIncompatiblePlatform=(BOOLEAN)|指定是否尝试操作，而不管存在的不兼容 SQL Server 平台。
|**/p:**|AllowUnsafeRowLevelSecurityDataMovement=(BOOLEAN)|如果此属性设置为 true，则不阻止具有行级别安全性的表上的数据运动。 默认值为 false。
|**/p:**|BackupDatabaseBeforeChanges=(BOOLEAN)|在部署任何更改之前，备份数据库。
|**/p:**|BlockOnPossibleDataLoss = (布尔值 True)|指定在 publish.operation 可能导致数据丢失的情况下，应终止发布集。
|**/p:**|BlockWhenDriftDetected = (布尔值 True)|指定是否阻止更新其架构与其注册不再匹配或已取消注册的数据库。
|**/p:**|CommandTimeout = (INT32"60")|指定针对 SQL Server 执行查询时的命令超时（以秒为单位）。
|**/p:**|CommentOutSetVarDeclarations=(BOOLEAN)|指定是否应在生成的发布脚本中注释掉 SETVAR 变量的声明。 如果您打算在发布时使用 SQLCMD.EXE 等工具指定命令行上的值，则可以选择这样做。
|**/p:**|CompareUsingTargetCollation=(BOOLEAN)|此设置指示在部署过程中如何处理数据库的排序规则；默认情况下，如果目标数据库的排序规则与源所指定的排序规则不匹配，就将更新目标数据库的排序规则。 设置此选项后，应使用目标数据库（或服务器）的排序规则。|
|**/p:**|CreateNewDatabase=(BOOLEAN)|指定当您发布到数据库时，是否应更新目标数据库或是否应删除并重新创建目标数据库。
|**/p:**|DatabaseEdition = ({Basic&#124;标准&#124;高级&#124;默认} Default)|定义版本的 Azure SQL 数据库。
|**/p:**|DatabaseMaximumSize=(INT32)|定义 Azure SQL 数据库的大小上限（以 GB 为单位）。
|**/p:**|DatabaseServiceObjective=(STRING)|定义 Azure SQL 数据库的性能级别，如“P0”或“S1”。
|**/p:**|DeployDatabaseInSingleUserMode=(BOOLEAN)|如果为 true，则数据库在部署前将设置为单用户模式。
|**/p:**|DisableAndReenableDdlTriggers = (布尔值 True)| 指定在发布过程开始时是否禁用数据定义语言 (DDL) 触发器，以及在发布操作结束时是否重新启用此类触发器。|
|**/p:**|DoNotAlterChangeDataCaptureObjects = (布尔值 True)|如果为 true，则不更改变更数据捕获对象。
|**/p:**|DoNotAlterReplicatedObjects = (布尔值 True)|指定是否在验证过程中标识重复的对象。
|**/p:**|DoNotDropObjectType=(STRING)|当 DropObjectsNotInSource 为 true 时不应删除的对象类型。 有效的对象类型名称为 Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers。
|**/p:**|DoNotDropObjectTypes=(STRING)|当 DropObjectsNotInSource 为 True 时不应删除的以分号分隔的对象类型列表。 有效的对象类型名称为 Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers。
|**/p:**|DropConstraintsNotInSource = (布尔值 True)|指定当发布到数据库时，是否将从目标数据库中删除数据库快照 (.dacpac) 文件中不存在的约束。|
|**/p:**|DropDmlTriggersNotInSource = (布尔值 True)|指定当发布到数据库时，是否将从目标数据库中删除数据库快照 (.dacpac) 文件中不存在的 DML 触发器。|
|**/p:**|DropExtendedPropertiesNotInSource = (布尔值 True)|指定在发布到数据库时，是否将从目标数据库中删除数据库快照 (.dacpac) 文件中不存在的扩展属性。|
|**/p:**|DropIndexesNotInSource = (布尔值 True)|指定当发布到数据库时，是否将从目标数据库中删除数据库快照 (.dacpac) 文件中不存在的索引。|
|**/p:**|DropObjectsNotInSource=(BOOLEAN)|指定当发布到数据库时，是否将从目标数据库中删除数据库快照 (.dacpac) 文件中不存在的对象。 此值优先于 DropExtendedProperties。|
|**/p:**|DropPermissionsNotInSource=(BOOLEAN)|指定当您更新到数据库时，是否将从目标数据库中删除数据库快照 (.dacpac) 文件中不存在的权限。|
|**/p:**|DropRoleMembersNotInSource=(BOOLEAN)|指定当您更新到数据库时，是否将从目标数据库中删除数据库快照 (.dacpac) 文件中未定义的角色成员。|
|**/p:**|DropStatisticsNotInSource = (布尔值 True)|指定当发布到数据库时，是否将从目标数据库中删除数据库快照 (.dacpac) 文件中不存在的统计信息。|
|**/p:**|ExcludeObjectType=(STRING)|应在部署期间忽略的对象类型。 有效的对象类型名称为 Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers。
|**/p:**|ExcludeObjectTypes=(STRING)|在部署期间应忽略的以分号分隔的对象类型列表。 有效的对象类型名称为 Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers。
|**/p:**|GenerateSmartDefaults=(BOOLEAN)|在使用一个不允许 Null 值的列更新一个包含数据的表时，自动提供默认值。
|**/p:**|IgnoreAnsiNulls = (布尔值 True)|指定在发布到数据库时，是应忽略还是应更新 ANSI NULLS 设置方面的差异。
|**/p:**|IgnoreAuthorizer=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新授权者方面的差异。
|**/p:**|IgnoreColumnCollation=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新列排序规则方面的差异。
|**/p:**|IgnoreColumnOrder=(BOOLEAN)|指定在发布到数据库时是否应忽略或更新表列顺序中的差异。|
|**/p:**|IgnoreComments=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新注释方面的差异。
|**/p:**|IgnoreCryptographicProviderFilePath = (布尔值 True)|指定在发布到数据库时，是应忽略还是应更新加密提供程序的文件路径方面的差异。
|**/p:**|IgnoreDdlTriggerOrder=(BOOLEAN)|指定在发布到数据库或服务器时，是应忽略还是更新数据定义语言 (DDL) 触发器中的顺序差异。|
|**/p:**|IgnoreDdlTriggerState=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新数据定义语言 (DDL) 触发器的启用状态或禁用状态方面的差异。|
|**/p:**|IgnoreDefaultSchema=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新默认架构方面的差异。|
|**/p:**|IgnoreDmlTriggerOrder=(BOOLEAN)|指定在发布到数据库时，是应忽略还是更新数据操作语言 (DML) 触发器中的顺序差异。|
|**/p:**|IgnoreDmlTriggerState=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新 DML 触发器的启用状态或禁用状态方面的差异。|
|**/p:**|IgnoreExtendedProperties=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新扩展属性方面的差异。|
|**/p:**|IgnoreFileAndLogFilePath = (布尔值 True)|指定在发布到数据库时，是应忽略还是应更新文件和日志文件路径方面的差异。|
|**/p:**|IgnoreFilegroupPlacement = (布尔值 True)|指定在发布到数据库时，是应忽略还是应更新 FILEGROUP 中的对象位置方面的差异。|
|**/p:**|IgnoreFileSize = (布尔值 True)|指定在发布到数据库时，是应忽略文件的大小差异，还是应发出警告。|
|**/p:**|IgnoreFillFactor = (布尔值 True)|指定在进行发布时，是应忽略索引存储的填充因子方面的差异，还是应发出警告。|
|**/p:**|IgnoreFullTextCatalogFilePath = (布尔值 True)|指定在发布到数据库时，是应忽略全文目录文件路径方面的差异，还是应发出警告。|
|**/p:**|IgnoreIdentitySeed=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新标识列种子方面的差异。|
|**/p:**|IgnoreIncrement=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新标识列增量方面的差异。|
|**/p:**|IgnoreIndexOptions=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新索引选项方面的差异。|
|**/p:**|IgnoreIndexPadding = (布尔值 True)|指定在发布到数据库时，是应忽略还是应更新索引填充方面的差异。|
|**/p:**|IgnoreKeywordCasing = (布尔值 True)|指定在发布到数据库时，是应忽略还是应更新关键字的大小写方面的差异。|
|**/p:**|IgnoreLockHintsOnIndexes=(BOOLEAN)|指定当您发布到数据库时，应忽略还是更新索引上的锁提示之间的差异。|
|**/p:**|IgnoreLoginSids = (布尔值 True)| 指定在发布到数据库时，是应忽略还是应更新安全标识号 (SID) 方面的差异。|
|**/p:**|IgnoreNotForReplication=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新不用于复制设置。|
|**/p:**|IgnoreObjectPlacementOnPartitionScheme = (布尔值 True)|指定在发布到数据库时，是应忽略还是应更新对象在分区方案中的位置。|
|**/p:**|IgnorePartitionSchemes=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新分区方案和分区函数方面的差异。|
|**/p:**|IgnorePermissions=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新权限方面的差异。|
|**/p:**|IgnoreQuotedIdentifiers = (布尔值 True)|指定在发布到数据库时，是应忽略还是应更新带引号的标识符设置方面的差异。|
|**/p:**|IgnoreRoleMembership=(BOOLEAN)|指定当您发布到数据库时，应忽略还是更新登录的角色成员身份之间的差异。|
|**/p:**|IgnoreRouteLifetime = (布尔值 True)|指定在发布到数据库时，应忽略还是应更新 SQL Server 保留路由表中的路由的时间量方面的差异。|
|**/p:**|IgnoreSemicolonBetweenStatements = (布尔值 True)|指定在发布到数据库时，是将忽略还是将更新 T-SQL 语句之间的分号差异。|
|**/p:**|IgnoreTableOptions=(BOOLEAN)|指定在发布到数据库时，是将忽略还是将更新表选项方面的差异。|
|**/p:**|IgnoreUserSettingsObjects=(BOOLEAN)|指定在发布到数据库时，是将忽略还是将更新用户设置对象方面的差异。|
|**/p:**|IgnoreWhitespace = (布尔值 True)|指定在发布到数据库时，是将忽略还是将更新空白方面的差异。|
|**/p:**|IgnoreWithNocheckOnCheckConstraints=(BOOLEAN)|指定在进行发布时，是将忽略还是将更新 CHECK 约束的 WITH NOCHECK 子句值方面的差异。|
|**/p:**|IgnoreWithNocheckOnForeignKeys=(BOOLEAN)|指定在发布到数据库时，是将忽略还是将更新外键的 WITH NOCHECK 子句值方面的差异。|
|**/p:**|IncludeCompositeObjects=(BOOLEAN)|将所有复合元素包含为单个发布操作的一部分。|
|**/p:**|IncludeTransactionalScripts=(BOOLEAN)|指定在发布到数据库时，是否应在可能的位置使用事务性语句。|
|**/p:**|NoAlterStatementsToChangeClrTypes=(BOOLEAN)|指定发布操作在存在差异时应始终删除并重新创建程序集，而不是发出 ALTER ASSEMBLY 语句。|
|**/p:**|PopulateFilesOnFileGroups = (布尔值 True)|指定当在目标数据库中创建新 FileGroup 时，是否也创建新文件。|
|**/p:**|RegisterDataTierApplication=(BOOLEAN)|指定是否向数据库服务器注册该架构。|
|**/p:**|RunDeploymentPlanExecutors=(BOOLEAN)|指定在执行其他操作时是否应运行 DeploymentPlanExecutor 参与者。|
|**/p:**|ScriptDatabaseCollation=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新数据库排序规则方面的差异。|
|**/p:**|ScriptDatabaseCompatibility=(BOOLEAN)|指定在发布到数据库时，是应忽略还是应更新数据库兼容性方面的差异。|
|**/p:**|ScriptDatabaseOptions = (布尔值 True)|指定是否应作为发布操作的一部分来设置或更新目标数据库属性。|
|**/p:**|ScriptDeployStateChecks=(BOOLEAN)|指定是否在发布脚本中生成声明，以验证数据库名称和服务器名称是否与数据库项目中指定的名称匹配。|
|**/p:**|ScriptFileSize=(BOOLEAN)|控制在向文件组添加文件时是否指定大小。|
|**/p:**|ScriptNewConstraintValidation = (布尔值 True)|在发布的末尾的所有约束将被验证为一组，避免数据错误检查或外的键约束在发布过程引起的。 如果设置为“False”，则将发布约束而不检查对应的数据。|
|**/p:**|ScriptRefreshModule = (布尔值 True)|在发布脚本的末尾包括刷新语句。|
|**/p:**|存储 = ({文件&#124;内存})|指定在生成数据库模型时如何存储元素。 出于性能原因，默认值为 InMemory。 对于大型数据库，需要备份了文件的存储。|
|**/p:**|TreatVerificationErrorsAsWarnings=(BOOLEAN)|指定验证过程中遇到的错误发布是否应视为警告。 在对目标数据库执行生成的部署计划之前，会先对该计划执行检查。 计划验证将检测仅有目标的对象（如索引）丢失等问题，必须解决这些问题以进行更改。 验证还检测以下情况：依赖项（如表或视图）因对复合项目的引用而存在，但未存在于目标数据库中。 您可以选择执行此操作以获取所有问题，而不是让第一个出错时停止发布操作的完整列表。|
|**/p:**|UnmodifiableObjectWarnings = (布尔值 True)|指定在无法修改的对象中发现差异（例如，如果文件的大小或路径存在差异）时是否生成警告。|
|**/p:**|VerifyCollationCompatibility = (布尔值 True)|指定是否验证排序规则兼容性。
|**/p:**|VerifyDeployment = (布尔值 True)|指定在出现可能阻止成功发布的问题的情况下，是否应在发布前执行将停止发布操作的检查。 例如，如果具有在数据库项目中不存在的目标数据库上的外键并且在发布时导致错误，则发布操作可能会停止。|
  
