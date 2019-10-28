---
title: 配置具有安全 Enclave 的 Always Encrypted | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 27f78de54735559365f771aaee3669b8f08856c7
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72902990"
---
# <a name="configure-always-encrypted-with-secure-enclaves"></a>配置具有安全 enclave 的 Always Encrypted

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[具有安全 enclave 的 Always Encrypted](always-encrypted-enclaves.md) 扩展现有 [Always Encrypted](always-encrypted-database-engine.md) 功能，以便对敏感数据启动更丰富的功能，同时保持数据的机密性。

若要设置包含安全 enclave 的 Always Encrypted，请使用以下工作流：

1. 配置主机保护者服务 (HGS) 证明。
2. 在 SQL Server 计算机上安装 [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)]。
3. 在客户端/开发计算机上安装工具。
4. 在 SQL Server 实例中配置 enclave 类型。
5. 预配已启用 enclave 的密钥。
6. 对包含敏感数据的列进行加密。

> [!NOTE]
> 有关如何在 SSMS 中设置测试环境并尝试使用具有安全 enclave 的 Always Encrypted 功能的分步教程，请参阅[教程：通过 SSMS 开始使用具有安全 enclave 的 Always Encrypted](../tutorial-getting-started-with-always-encrypted-enclaves.md)。

## <a name="configure-your-environment"></a>配置环境

必须在环境中安装 Windows Server 2019 Preview 和 SQL Server Management Studio (SSMS) 18.0、.NET Framework 以及其他一些组件，才能结合使用安全 enclave 和 Always Encrypted。 以下部分提供了获取所需组件的详细信息和链接。

### <a name="sql-server-computer-requirements"></a>SQL Server 计算机要求

运行 SQL Server 的计算机需要以下操作系统和 SQL Server 版本：

 SQL Server：

- [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] 或更高版本

 Windows：

- Windows 10 企业版，版本 1809
- Windows Server DataCenter（半年频道），版本 1809
- Windows Server 2019 DataCenter

> [!IMPORTANT]
> SQL Server 计算机必须配置为受保护的主机，由 HGS 进行检验证明。 TPM 证明是建议的针对生产环境的 enclave 证明方法，需要在物理计算机，而不是虚拟机上运行 SQL Server。 虚拟机仅适用于预生产环境。

### <a name="hgs-computer-requirements"></a>HGS 计算机要求

在测试和原型设计过程中，单台 HGS 计算机已足够。 对于生产环境，建议使用含 3 台计算机的 Windows 故障转移群集。

Windows 主机保护者服务 (HGS) 需要在单独的 HGS 计算机上安装，而不是安装在与 SQL Server 相同的计算机上。 若要详细了解 HGS 计算机要求和设置，请参阅[在 SQL Server 中设置用于 Always Encrypted 的主机保护者服务](https://docs.microsoft.com/windows-server/security/set-up-hgs-for-always-encrypted-in-sql-server)。


### <a name="determine-your-attestation-service-url"></a>确定证明服务 URL

若要确定证明服务 URL，需要配置工具和应用程序：

1. 以管理员身份登录 SQL Server 计算机。
2. 以管理员身份运行 PowerShell。
3. 运行 [Get-hgsclientconfiguration](https://docs.microsoft.com/powershell/module/hgsclient/get-hgsclientconfiguration)。
4. 编写并保存 AttestationServerURL 属性。 这看起来应类似于 `https://x.x.x.x/Attestation`。

### <a name="install-tools"></a>安装工具

在客户端/开发计算机上安装以下工具：

1. [.NET Framework 4.7.2](https://www.microsoft.com/net/download/dotnet-framework-runtime)。
2. [SSMS 18.0 或更高版本](../../../ssms/download-sql-server-management-studio-ssms.md)。
3. [SQL Server PowerShell 模块](../../../powershell/download-sql-server-ps-module.md)版本 21.1 或更高版本。
4. [Visual Studio（建议使用 2017 或更高版本）](https://visualstudio.microsoft.com/downloads/)。
5. [.NET Framework 4.7.2 开发人员工具包](https://www.microsoft.com/net/download/visual-studio-sdks)。
6. [Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider NuGet 包](https://www.nuget.org/packages/Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider)，2.2.0 或更高版本。
7. [Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders NuGet 包](https://www.nuget.org/packages?q=Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders)。

使用 Visual Studio 项目 NuGet 包，以使用含安全 enclave 的 Always Encrypted 来开发应用程序。 只有在 Azure Key Vault 中存储列主密钥，才需要第一个包。 有关详细信息，请参阅[开发应用程序](#develop-applications-issuing-rich-queries-in-visual-studio)。

### <a name="configure-a-secure-enclave"></a>配置安全 enclave

在客户端/开发计算机上：

1. 以 Active Directory (AD) 管理员身份打开 SSMS 并连接到 SQL Server 实例。
2. 若要验证实例中是否支持具有安全 enclave 的 Always Encrypted，请运行以下查询：

   ```sql
   SELECT [name], [value], [value_in_use] FROM sys.configurations
   WHERE [name] = 'column encryption enclave type';
   ```

    查询应返回类似于以下的行：  

    | NAME                           | 值 | value_in_use |
    | ------------------------------ | ----- | -------------|
    | 列加密 enclave 类型 | 0     | 0            |

3. 向 VBS enclave 配置安全 enclave 类型。

   ```sql
   EXEC sys.sp_configure 'column encryption enclave type', 1;
   RECONFIGURE;
   ```

4. 重新启动 SQL Server 实例，以前的更改才会生效。 可在“对象资源管理器”中右键单击实例并选择“重启”，从而在 SSMS 中重启实例。 重启实例后，请重新连接到它。

5. 通过运行以下查询确认现已加载安全 enclave：

   ```sql
   SELECT [name], [value], [value_in_use] FROM sys.configurations
   WHERE [name] = 'column encryption enclave type';
   ```   

    查询应返回类似于以下的行：  

    | NAME                           | 值 | value_in_use |
    | ------------------------------ | ----- | -------------- |
    | 列加密 enclave 类型 | 1     | 1              |

6. 若要启用对加密列的大量计算，请运行以下查询：

   ```sql
   DBCC traceon(127,-1);
   ```

    > [!NOTE]
    > 默认情况下，[!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] 中禁用了大量计算。 每次重启 SQL Server 实例之后，都需要使用上述语句启用它们。

## <a name="provision-enclave-enabled-keys"></a>预配已启用 enclave 的密钥

引入已启用 enclave 的密钥不会从根本上改变 [Always Encrypted 密钥预配和密钥管理工作流](overview-of-key-management-for-always-encrypted.md)。 只会改变列主密钥预配工作流。 现在可以将密钥标记为已启用 enclave。默认情况下，列主密钥未启用 enclave。 如果将新的列主密钥设置为已启用 enclave（使用 SSMS 或 PowerShell），便会发生以下情况：

- 设置数据库的列主密钥元数据中的 `ENCLAVE_COMPUTATIONS` 属性。
- 对列主密钥属性值（包括 `ENCLAVE_COMPUTATIONS` 设置）进行数字签名。 此工具将添加签名，该签名是使用元数据的实际列主密钥生成的。 此签名可防止恶意篡改 `ENCLAVE_COMPUTATIONS` 设置。 SQL 客户端驱动程序验证签名之后才会允许使用 enclave。 这使安全管理员能够控制可以在 enclave 内计算哪些列数据。

列主密钥的 `ENCLAVE_COMPUTATIONS` 属性不可变。 在预配密钥后，便无法更改此属性。 不过，可以用 `ENCLAVE_COMPUTATIONS` 属性值与原始密钥不同的新密钥来替换列主密匙。 若要替换列主密钥，请[轮换列主密钥](#make-columns-enclave-enabled-by-rotating-their-column-master-key)。 若要详细了解 `ENCLAVE_COMPUTATIONS` 属性，请参阅 [CREATE COLUMN MASTER KEY](../../../t-sql/statements/create-column-master-key-transact-sql.md)。

若要预配已启用 enclave 的列加密密钥，需要确保加密列加密密钥的列主密钥已启用 enclave。

当前，以下限制适用于预配已启用 enclave 的密钥：

- 已启用 enclave 的列主密钥必须存储在 [Windows 证书存储](/windows/desktop/seccrypto/managing-certificates-with-certificate-stores)或 [Azure Key Vault](/azure/key-vault/key-vault-whatis/) 中。 暂不支持将已启用 enclave 的列主密钥存储在其他类型的密钥存储（例如，硬件安全模块或自定义密钥存储）中。

### <a name="provision-enclave-enabled-keys-using-sql-server-management-studio-ssms"></a>使用 SQL Server Management Studio (SSMS) 预配已启用 enclave 的密钥

以下步骤创建已启用 enclave 的密钥（需要 SSMS 18.0 或更高版本）：

1. 使用 SSMS 连接到你的数据库。
2. 在“对象资源管理器”中，展开数据库，然后导航到“安全” > “Always Encrypted 密钥”    。
3. 预配已启用 enclave 的新列主密钥：

    1. 右键单击“Always Encrypted 密钥”，然后选择“新列主密钥...”   。
    2. 选择列主密钥名称。
    3. 请确保选择“Windows 证书存储(当前用户或本地计算机)”  或“Azure Key Vault”  。
    4. 选择“允许 enclave 计算”  。
    5. 如果选择了 Azure Key Vault，请登录到 Azure 并选择密钥保管库。 若要深入了解如何创建 Always Encrypted 的密钥保管库，请参阅 [Manage your key vaults from Azure portal](https://blogs.technet.microsoft.com/kv/2016/09/12/manage-your-key-vaults-from-new-azure-portal/)（从 Azure 门户管理密钥保管库）。
    6. 如已存在，则请选择密钥，或按照窗体上的说明创建新密钥。
    7. 单击“确定”  。

        ![允许 enclave 计算](./media/always-encrypted-enclaves/allow-enclave-computations.png)

4. 创建已启用 enclave 的新列加密密钥：

    1. 右键单击“Always Encrypted 密钥”，然后选择“新建列加密密钥”   。
    2. 输入新列加密密钥的名称。
    3. 在“列主密匙”下拉列表中，选择在上一步骤创建的列主密钥  。
    4. 单击“确定”  。

### <a name="provision-enclave-enabled-keys-using-powershell"></a>使用 PowerShell 预配已启用 enclave 的密钥

以下各节提供示例 PowerShell 脚本来预配已启用 enclave 的密钥。 将突出显示特定于具有安全 enclave 的 Always Encrypted 的（新）步骤。 有关使用 PowerShell 预配密钥的详细信息（不特定于具有安全 enclave 的 Always Encrypted），请参阅[使用 PowerShell 配置 Always Encrypted](configure-always-encrypted-keys-using-powershell.md)。

#### <a name="provisioning-enclave-enabled-keys---windows-certificate-store"></a>预配已启用 enclave 的密钥 - Windows 证书存储

在客户端/开发计算机上，打开 Windows PowerShell ISE，并运行以下脚本。

特别要注意的是使用 [New-SqlCertificateStoreColumnMasterKeySettings  ](https://docs.microsoft.com/powershell/module/sqlserver/new-sqlcertificatestorecolumnmasterkeysettings) cmdlet 中的 `-AllowEnclaveComputations` 参数。

```powershell
# Create a column master key in Windows Certificate Store.
$cert = New-SelfSignedCertificate -Subject "\<Subject Name\>" -CertStoreLocation Cert:CurrentUser\\My -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage DataEncipherment -KeySpec KeyExchange

# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database. Provide the server/db name. Modify the connection string, if needed.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Data Source = " + $serverName + "; Initial Catalog = " + $databaseName + "; Integrated Security = true"
$database = Get-SqlDatabase -ConnectionString $connStr

# Create a SqlColumnMasterKeySettings object for your column master key
# using the -AllowEnclaveComputations parameter.
$cmkSettings = New-SqlCertificateStoreColumnMasterKeySettings -CertificateStoreLocation "CurrentUser" -Thumbprint $cert.Thumbprint -AllowEnclaveComputations

# Create column master key metadata in the database.
$cmkName = "<column master key name in the database>"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database.
$cekName = "<column encryption key name in the database>"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName
```

#### <a name="provisioning-enclave-enabled-keys---azure-key-vault"></a>预配已启用 enclave 的密钥 - Azure Key Vault

在客户端/开发计算机上，打开 Windows PowerShell ISE，并运行以下脚本。

**步骤 1：在 Azure Key Vault 中预配列主密钥**

还可以使用 Azure 门户执行此操作。 有关详细信息，请参阅[通过 Azure 门户管理密钥保管库](https://blogs.technet.microsoft.com/kv/2016/09/12/manage-your-key-vaults-from-new-azure-portal/)。


```powershell
Import-Module Az
Connect-AzAccount

# User values
$SubscriptionId = "<Azure SubscriptionId>"
$resourceGroup = "<resource group name>"
$azureLocation = "<datacenter location>"
$akvName = "<key vault name>"
$akvKeyName = "<key name>"

# Set the context to the specified subscription.
$azureCtx = Set-AzContext -SubscriptionId $SubscriptionId

# Create a new resource group - skip, if your desired group already exists.
New-AzResourceGroup -Name $resourceGroup -Location $azureLocation

# Create a new key vault - skip if your vault already exists.
New-AzKeyVault -VaultName $akvName -ResourceGroupName $resourceGroup -Location $azureLocation

# Grant yourself permissions needed to create and use the column master key.
Set-AzKeyVaultAccessPolicy -VaultName $akvName -ResourceGroupName $resourceGroup -PermissionsToKeys get, create, list, update, wrapKey,unwrapKey, sign, verify -UserPrincipalName $azureCtx.Account

# Create a column master key in Azure Key Vault.
$akvKey = Add-AzureKeyVaultKey -VaultName $akvName -Name $akvKeyName -Destination "Software"
```

**步骤 2：在数据库中创建列主密钥元数据、创建列加密密钥以及在数据库中创建列加密密钥元数据**


```powershell
# Import the SqlServer module.
Import-Module "SqlServer" -Version

# Connect to your database. Provide the server and db name. If needed, modify the connection string.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Data Source = " + $serverName + "; Initial Catalog = " + $databaseName + "; Integrated Security = true"
$database = Get-SqlDatabase -ConnectionString $connStr

# Authenticate to Azure before calling New-SqlAzureKeyVaultColumnMasterKeySettings,
# because -AllowEnclaveComputations causes a call to Azure Key Vault
# to generate the signature of the column master key.
Add-SqlAzureAuthenticationContext -Interactive

# Create a SqlColumnMasterKeySettings object for your column master key.
$cmkSettings = New-SqlAzureKeyVaultColumnMasterKeySettings -KeyURL $akvKey.ID -AllowEnclaveComputations

# Create column master key metadata in the database.
$cmkName = "<column master key name in the database>"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database.
$cekName = "<column encryption key name in the database>"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName
```

## <a name="identify-enclave-enabled-keys-and-columns"></a>标识已启用 enclave 的密钥和列

若要列出在数据库中配置的列主密匙，请查询 [sys.column_master_keys](../../system-catalog-views/sys-column-master-keys-transact-sql.md) 目录视图（例如，在 SSMS 中）。 新列“allow_enclave_computations”  指明列主密钥是否已启用 enclave。

```sql
SELECT name, allow_enclave_computations
FROM sys.column_master_keys;
```

如果列加密密钥是使用已启用 enclave 的列加密密钥进行加密，表明它已启用 enclave。 下面的查询联接 [sys.column_master_keys](../../system-catalog-views/sys-column-master-keys-transact-sql.md)、[sys.column_encryption_key_values](../../system-catalog-views/sys-column-encryption-key-values-transact-sql.md) 和 [sys.column_encryption_keys](../../system-catalog-views/sys-column-encryption-keys-transact-sql.md)，以返回已启用 enclave 的列加密密钥。

```sql
SELECT cek.name AS [cek_name]
, cmk.name AS [cmk_name]
, cmk.allow_enclave_computations
FROM sys.column_master_keys cmk
JOIN sys.column_encryption_key_values cekv
   ON cmk.column_master_key_id = cekv.column_master_key_id
JOIN sys.column_encryption_keys cek
   ON cekv.column_encryption_key_id = cek.column_encryption_key_id;
```

如果列是使用已启用 enclave 的密钥进行加密，表明它已启用 enclave。 若要确定哪些列已启用 enclave，请使用以下查询：

```sql
SELECT c.name AS column_name
, cek.name AS cek_name
, cmk.name AS [cmk_name]
, cmk.allow_enclave_computations
from sys.columns c
JOIN sys.column_encryption_keys cek 
ON c.column_encryption_key_id = cek.column_encryption_key_id 
JOIN sys.column_encryption_key_values cekv 
ON cekv.column_encryption_key_id = cek.column_encryption_key_id 
JOIN sys.column_master_keys cmk 
ON cmk.column_master_key_id = cekv.column_master_key_id;
```

## <a name="manage-collations"></a>管理排序规则

Always Encrypted 限制排序规则。 禁止对使用确定性加密进行加密的字符串列使用非 BIN2 排序规则。 此限制也适用于已启用 enclave 的字符串列。

非 BIN2 排序规则可用于使用随机加密和启用了 enclave 的列加密密钥加密的字符串列。 但是，可用于此类列的唯一新功能是就地加密。 若要启用丰富计算（模式匹配、比较运算），必须对加密列使用 BIN2 排序规则。

下表汇总了已启用 enclave 的字符串列的功能，具体取决于加密类型和排序规则排序顺序。

| **排序规则排序顺序** | **确定性加密** | **随机加密**                 |
| ------------------------ | ---------------------------- | ----------------------------------------- |
| **非 BIN2**             | 不支持                | 就地加密                       |
| **BIN2**                 | 等式比较          | 就地加密和丰富计算 |

### <a name="determining-and-changing-collations"></a>确定和更改排序规则

在 SQL Server 中，可以在服务器、数据库或列级别设置排序规则。 有关如何确定当前排序规则和更改服务器、数据库或列级别排序规则的常规说明，请参阅[排序规则和 Unicode 支持](../../collations/collation-and-unicode-support.md)。

### <a name="special-considerations-for-non-unicode-string-columns"></a>关于非 UNICODE 字符串列的特殊注意事项

由 SQL 客户端驱动程序中的限制（与 Always Encrypted 无关）施加的以下附加限制适用于非 UNICODE (ASCII) 字符串列。 如果覆盖非 UNICODE（char、varchar）字符串列的数据库排序规则，必须确保列排序规则将相同的代码页作为数据库排序规则使用。
若要列出所有排序规则及其代码页标识符，请使用以下查询：

```sql
SELECT [Name]
   , [Description]
   , [CodePage] = COLLATIONPROPERTY([Name], 'CodePage')
FROM ::fn_helpcollations();
```

例如，`Chinese_Traditional_Stroke_Order_100_CI_AI_WS` 和 `Chinese_Traditional_Stroke_Order_100_BIN2` 有相同的代码页 (950)，而 `Chinese_Traditional_Stroke_Order_100_CI_AI_WS` 和 `Latin1_General_100_BIN2` 则有不同的代码页（分别为 950 和 1252）。 上述限制不适用于 UNICODE（`nchar`、`nvarchar`）字符串列。 建议为要创建的新加密列设置 UNICODE 数据类型，或在加密现有列前先将类型更改为 UNICODE 类型。

## <a name="create-a-new-table-with-enclave-enabled-columns"></a>新建包含已启用 enclave 的列的表

可以使用 [CREATE TABLE (Transact-SQL)](../../../t-sql/statements/create-table-transact-sql.md) 语句创建一个带加密列的新表。 含安全 enclave 的 Always Encrypted 不会更改此语句的语法。

1. 使用 SSMS 连接到数据库，并打开查询窗口。

     > [!NOTE]
     > 无需在此任务的连接字符串中启用 Always Encrypted。

2. 在查询窗口中，发出 `CREATE TABLE` 语句来新建表，同时在要加密的每个列的[列定义](../../../t-sql/statements/alter-table-column-definition-transact-sql.md)中指定 `ENCRYPTED WITH` 子句。 若要使列启用 enclave，请确保指定已启用 enclave 的列加密密钥。 如果数据库的默认排序规则不是 BIN2 排序规则，可能还需要为字符串列指定 BIN2 排序规则。 请参阅“排序规则设置”部分了解详细信息。

### <a name="example-of-creating-a-new-table-with-enclave-enabled-columns"></a>示例：新建包含已启用 enclave 的列的表

以下语句创建一个包含两个加密列的新表，分别为 SSN 和 Salary。 假设 CEK1 是已启用 enclave 的列加密密钥，SQL Server 引擎支持两个列的就地加密和丰富计算，因为列使用随机加密。 该语句为 UNICODE SSN 列设置 Latin1\_General\_BIN2，这是假定默认数据库排序规则为非 BIN2 Latin1 排序规则的必要条件。

```sql
CREATE TABLE [dbo].[Employees]
(
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [SSN] [char](11) COLLATE Latin1_General_BIN2 ENCRYPTED WITH (
        COLUMN_ENCRYPTION_KEY = [CEK1],
        ENCRYPTION_TYPE = Randomized,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [Salary] [money] ENCRYPTED WITH (
        COLUMN_ENCRYPTION_KEY = [CEK1],
        ENCRYPTION_TYPE = Randomized,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
    CONSTRAINT [PK_dbo.Employees] PRIMARY KEY CLUSTERED (
[EmployeeID] ASC
)
) ON [PRIMARY];
GO
```

## <a name="add-a-new-enclave-enabled-column-to-an-existing-table"></a>将已启用 enclave 的新列添加到现有表

可以使用 [ALTER TABLE (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md) / ADD 语句将新加密列添加到现有表。 含安全 enclave 的 Always Encrypted 不会更改此语句的语法。

1. 使用 SSMS 连接到数据库，并打开查询窗口。

   对于此任务，无需在连接字符串中启用 Always Encrypted。

2. 在查询窗口中，发出带有 ADD 子句的 ALTER TABLE 语句，在[列定义](../../../t-sql/statements/alter-table-column-definition-transact-sql.md)中指定 ENCRYPTED WITH 子句，并使用已启用 enclave 的列加密密钥。 如果新列是字符串列，且数据库的默认排序规则不是 BIN2 排序规则，可能还需要指定 BIN2 排序规则。 请参阅“排序规则设置”部分了解详细信息。

### <a name="example-of-adding-a-new-enclave-enabled-column-to-an-existing-table"></a>示例：将已启用 enclave 的新列添加到现有表

假设 CEK1 是已启用 enclave 的列加密密钥，以下语句将添加一个名为“BirthDate”的新加密列，后者支持丰富查询和就地加密（如列使用随机加密）。

```sql
ALTER TABLE [dbo].[Employees]
ADD [BirthDate] [Date] ENCRYPTED WITH (
COLUMN_ENCRYPTION_KEY = [CEK1],
ENCRYPTION_TYPE = Randomized,
ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NULL;
```


## <a name="prepare-an-ssms-query-window-with-always-encrypted-enabled"></a>准备已启用 Always Encrypted 的 SSMS 查询窗口

若要添加所需的连接参数来启用 enclave 计算：

1. 打开 SSMS。
2. 在“连接到服务器”对话框中指定服务器名称和数据库名称后，单击“选项”  。 导航到“Always Encrypted”  选项卡，选择“启用 Always Encrypted”  ，然后指定 enclave 证明 URL。
    
    ![列加密设置](./media/always-encrypted-enclaves/column-encryption-setting.png)

3. 单击“连接”。
4. 打开一个新的查询窗口。

或者，如果已打开查询窗口，下面将引导你如何更新其数据库连接以启用 Always Encrypted：

1. 右键单击现有查询窗口中的任意位置。
2. 选择“连接”\>“更改连接”。
3. 单击“选项”  。 导航到“Always Encrypted”  选项卡，选择“启用 Always Encrypted”  ，然后指定 enclave 证明 URL。
4. 单击“连接”。

## <a name="work-with-encrypted-columns"></a>使用加密列

### <a name="encrypt-an-existing-plaintext-column-in-place"></a>就地加密现有纯文本列

可以使用 [ALTER TABLE (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md) / ALTER COLUMN 语句就地加密现有纯文本列，前提是你使用已启用 enclave 的列加密密钥。

若要使用未启用 enclave 的密钥加密列，必须使用客户端工具，如 SSMS 中的 Always Encrypted 向导，或 SqlServer PowerShell 模块中的 Set-SqlColumnEncryption cmdlet。 有关详细信息，请参阅：

- [始终加密向导](always-encrypted-wizard.md)
- [使用 PowerShell 配置列加密](configure-column-encryption-using-powershell.md)


#### <a name="prerequisites-for-encrypting-an-existing-plaintext-column-in-place"></a>就地加密现有纯文本列的先决条件

- 未加密现有列。
- 已预配启用了 enclave 的密钥。
- 你有权访问列主密钥。

#### <a name="steps-for-encrypting-existing-plaintext-column-in-place"></a>就地加密现有纯文本列的步骤

1. 准备一个 SSMS 查询窗口，同时在数据库连接中启用 Always Encrypted 和 enclave 计算。 有关详细信息，请参阅[准备一个启用了 Always Encrypted 的 SSMS 查询窗口](#prepare-an-ssms-query-window-with-always-encrypted-enabled)。
2. 在查询窗口中，发出带有 ALTER COLUMN 子句的 ALTER TABLE 语句，在 ENCRYPTED WITH 子句中指定启用了 enclave 列的加密密钥。 如果列为字符串列（例如，char、varchar、nchar、nvarchar），可能还需要将排序规则更改为 BIN2 排序规则。 请参阅“排序规则设置”部分了解详细信息。
    
    > [!NOTE]
    > 如果列主密钥存储在 Azure Key Vault 中，系统可能会提示你登录到 Azure。

3. 清除访问表的所有批处理和存储过程的计划缓存，以刷新参数加密信息。 
 
    ```sql
    ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
    ```
    > [!NOTE]
    > 如果不从缓存中删除受影响的查询计划，加密后首次执行查询可能会失败。

    > [!NOTE]
    > 请谨慎使用 `ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE` 或 `DBCC FREEPROCCACHE` 来清除计划缓存，因为这可能会导致查询性能暂时降低。 若要使清除缓存的负面影响降到最低，可以选择性地仅删除受影响的查询计划。

4.  调用 [sp_refresh_parameter_encryption](../../system-stored-procedures/sp-refresh-parameter-encryption-transact-sql.md) 来更新每个模块（存储过程、函数、视图、触发器）的参数元数据，这些参数暂留在 [sys.parameters](../..//system-catalog-views/sys-parameters-transact-sql.md) 中，并且可能已通过加密列而失效。

#### <a name="example-of-encrypting-existing-plaintext-column-in-place"></a>示例：就地加密现有纯文本列

下面的示例假定：

- CEK1 是已启用 enclave 的列加密密钥。

- SSN 列为纯文本，且当前使用的是 Latin1，非 BIN2 排序规则（例如，Latin1\_General\_CI\_AI\_KS\_WS）。

该语句使用随机加密和已启用 enclave 的列加密密钥对 SSN 列进行加密。 它还使用相应的（在相同代码页）BIN2 排序规则覆盖默认数据库排序规则。

联机执行该操作 (ONLINE = ON)。 另请注意，调用重新创建查询计划的 ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE  受到表架构更改影响。

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char] COLLATE Latin1_General_BIN2
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
WITH
(ONLINE = ON);
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

### <a name="make-an-existing-encrypted-column-enclave-enabled"></a>为现有加密列启用 enclave

若要为未启用 enclave 的现有列启用 enclave 功能，具体方法有多种。 选择哪种方法取决于以下几个因素：

- **作用域/粒度：** 你是否想要为列子集或使用给定列主密钥保护的所有列启用 enclave 功能？
- **数据大小：** 包含要启用 enclave 的列的表的大小是多少？
- 此外，是否要更改列的加密类型？ 请记住，唯一的随机的加密支持丰富计算（模式匹配、比较运算符）。 如果列是使用确定性加密进行加密，你还需要使用随机加密对它进行重新加密，才能解锁 enclave 的全部功能。

下面是用于为现有列启用 enclave 的三种方法：

#### <a name="option-1-rotate-the-column-master-key-to-replace-it-with-an-enclave-enabled-column-master-key"></a>选项 1：轮换列主密钥，将其替换为已启用 enclave 的列主密钥。
  
- 优点：
  - 不涉及重新加密数据，因此这种方法通常是最快的。 建议对包含大量数据的列使用这种方法，但前提是需要为之启用丰富计算的所有列已使用确定性加密，因此无需重新加密。
  - 可以按规模对多个列启用 enclave 功能，因为它可以为与原始列主密匙相关联的所有列加密密钥和所有加密列启用 enclave。
  
- 缺点：
  - 不支持将加密类型从确定性加密更改为随机加密。因此，虽然可以为使用确定性加密的列解锁就地加密功能，但无法启用丰富计算。
  - 禁止选择性地转换一些与给定列主密钥关联的列。
  - 产生密钥管理开销 - 需要创建新的列主密钥并使其可用于查询受影响列的应用程序。  

#### <a name="option-2-this-approach-involves-two-steps-1-rotating-the-column-master-key-as-in-option-1-and-2-re-encrypting-a-subset-of-deterministically-encrypted-columns-using-randomized-encryption-to-enable-rich-computations-for-those-columns"></a>选项 2：此方法包括两个步骤：1 ) 轮换列主密钥（如选项 1 所示）和 2 ) 使用随机加密重新加密通过确定性加密的列子集，以便为这些列启用丰富计算。
  
- 优点：
  - 就地重新加密数据，因此对于包含大量数据的确定性加密列，它是启用丰富查询的建议方法。 由于第 1 步为使用确定性加密的列解锁就地加密功能，因此第 2 步可以就地执行。
  - 可以大规模地为多个列启用 enclave 功能。
  
- 缺点：
  - 禁止选择性地转换一些与给定列主密钥关联的列。
  - 它会产生密钥管理开销 - 需要创建新的列主密钥并使其可用于查询受影响列的应用程序。

#### <a name="option-3-re-encrypting-selected-columns-with-a-new-enclave-enabled-column-encryption-key-and-randomized-encryption-if-needed-on-the-client-side"></a>选项 3：在客户端上使用新的已启用 enclave 的列加密密钥和随机加密（如果需要）重新加密所选的列。
  
- 优点 - 此方法：
  - 可以选择性地为一个列或小型列子集启用 enclave 功能。
  - 可以在一个步骤中为确定性加密列启用丰富计算。
  - 由于无需新建列主密钥，因此它对应用程序的影响较小。
  
- 缺点：
  - 包含列的表的整个内容都需要移至数据库之外以进行重新加密，因此建议仅用于小型表。

有关详细信息，请参阅以下部分：
  - [通过轮换其列主密钥为列启用 Enclave](#make-columns-enclave-enabled-by-rotating-their-column-master-key)
  - [就地重新加密列](#re-encrypt-columns-in-place)
  - [在客户端重新加密列](#re-encrypt-columns-on-the-client-side)

### <a name="make-columns-enclave-enabled-by-rotating-their-column-master-key"></a>通过轮换列主密钥为列启用 enclave

列主密钥轮替是将现有列主密钥替换为新列主密钥的过程。 这涉及到使用新列主密钥重新加密与旧列主密钥相关联的列加密密钥。 自 Always Encrypted 的初始版本发布以来，此工作流便一直存在，以支持替换列主密钥，从而满足合规性和安全性方面的需求（以防现有列主密钥遭泄露）。

使用 enclave 的 Always Encrypted 为列主密钥轮换工作流添加了新用途。 假设旧列主密钥未启用 enclave，而新列主密钥已启用 enclave，那么轮换过程可以为所有与列主密钥相关联的列加密密钥有效启用 enclave。 由于轮换列主密钥不涉及重新加密数据，因此建议使用这一过程为现有列启用 enclave 功能。

轮换列主密钥不会更改受影响列的加密类型。 因此，它只能解锁确定性加密列的就地加密。 若要使用确定性加密解锁列的丰富计算，需要在轮换列主密钥后，对其进行重新加密（就地）。

可能还需要使用随机加密将字符串列的排序规则更改为 BIN2 排序规则，才能解锁丰富计算。 请参阅“排序规则设置”部分了解详细信息。

列主密钥轮换过程是相同的，而不考虑所涉及的任一密钥是否已启用 enclave。 有关如何轮换列主密钥的详细信息，请参阅以下文章：

- [使用 SSMS 轮换列主密钥](configure-always-encrypted-using-sql-server-management-studio.md)
- [使用 PowerShell 轮换列主密钥](rotate-always-encrypted-keys-using-powershell.md)

为方便起见，下面提供了用于轮换列主密钥的 PowerShell 脚本示例。

#### <a name="prerequisites-of-rotating-the-column-master-key-for-enclave-enabled-columns"></a>为已启用 enclave 的列轮换列主密钥的先决条件

- 已预配新的已启用 enclave 的列主密钥。
- 有权访问旧的和新的列主密钥。
- 使用旧的列主密钥保护的所有字符串列都使用 BIN2 排序规则。

> [!NOTE]
> 也可以在轮换列主密钥后更改字符串列的排序规则。

#### <a name="steps-for-rotating-the-column-master-key-for-enclave-enabled-columns"></a>为已启用 enclave 的列轮换列主密钥的步骤

将以下脚本粘贴到 Windows PowerShell ISE 中，将\<占位符\>替换为特定值：

```powershell
# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database. Modify server/db name or/and the connection string, if needed.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Data Source = " + $serverName + "; Initial Catalog = " +
$databaseName + "; Integrated Security = true"
$database = Get-SqlDatabase -ConnectionString $connStr

# Set the names of the old/current column master key and the new/target enclave-enabled column master key. (Change the names, if needed).
$oldCmkName = "<old column master key name>"
$newCmkName = "<new column master key name>"

# Authenticate to Azure. Needed only of either column master key is stored in Azure Key Vault.
Add-SqlAzureAuthenticationContext -Interactive

# Initiate the rotation from the current column master key to the new column master key.
Invoke-SqlColumnMasterKeyRotation -SourceColumnMasterKeyName $oldCmkName
-TargetColumnMasterKeyName $newCmkName -InputObject $database

# Complete the rotation of the old column master key.
Complete-SqlColumnMasterKeyRotation -SourceColumnMasterKeyName
$oldCmkName -InputObject $database

# Remove the old column master key metadata.
Remove-SqlColumnMasterKey -Name $oldCmkName -InputObject $database
```


### <a name="re-encrypt-columns-in-place"></a>就地重新加密列

在为列启用 enclave 之后，可以就地执行下列操作（在 enclave 内部，无需将数据移出数据库）：

- 例如，轮换列加密密钥（使用新密钥替换它）以遵守法规遵从性要求，某些规定要求定期轮换密钥，或者出于安全考虑（以防列加密密钥遭泄漏）。
- 更改加密类型（例如从确定性加密改为随机加密），以解锁列的丰富计算。

#### <a name="prerequisites-for-re-encrypting-columns-in-place"></a>就地重新加密列的先决条件

- 使用已启用 enclave 的列加密密钥对列进行加密。
- 已预配新的已启用 enclave 的列加密密钥（如果你的目标是要替换当前已启用 enclave 的列加密密钥，进而保护列）。
- 你有权访问列主密钥。

#### <a name="steps-for-re-encrypting-columns-in-place"></a>就地重新加密列的步骤

1. 准备一个 SSMS 查询窗口，同时为数据库连接启用 Always Encrypted 和 enclave 计算。 有关详细信息，请参阅[准备一个启用了 Always Encrypted 的 SSMS 查询窗口](#prepare-an-ssms-query-window-with-always-encrypted-enabled)。

2. 在查询窗口中，请求将 [ALTER TABLE (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md) 语句与 ALTER COLUMN 子句结合使用，以便在 ENCRYPTED WITH 子句中指定以下内容：
    
    1. 已启用 enclave 的新列加密密钥的名称（若要轮换当前密钥）。 如果不要更改列加密密钥，需要指定当前密钥的名称。
    
    2. 新加密类型（若要更改加密类型）。 如果不要更改加密类型，需要指定当前加密类型。
        
       如果要重新加密的列使用的排序规则 (BIN2) 不同于默认数据库排序规则，需要添加 COLLATE 短语，并在列定义中指定当前列排序规则（以保持排序规则不变）。
        
       > [!NOTE]
       > 如果列主密钥存储在 Azure Key Vault 中，系统可能会提示你登录到 Azure。

3. 清除访问表的所有批处理和存储过程的计划缓存，以刷新参数加密信息。 
 
    ```sql
    ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
    ```
    > [!NOTE]
    > 如果不从缓存中删除受影响的查询计划，加密后首次执行查询可能会失败。

    > [!NOTE]
    > 请谨慎使用 ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE 或 DBCC FREEPROCCACHE 来清除计划缓存，因为这可能会导致查询性能暂时降低。 若要使清除缓存的负面影响降到最低，可以选择性地仅删除受影响的查询计划。

4.  调用 [sp_refresh_parameter_encryption](../../system-stored-procedures/sp-refresh-parameter-encryption-transact-sql.md) 来更新每个模块（存储过程、函数、视图、触发器）的参数元数据，这些参数暂留在 [sys.parameters](../..//system-catalog-views/sys-parameters-transact-sql.md) 中，并且可能已通过重新加密列而失效。

#### <a name="examples-of-re-encrypting-columns-in-place"></a>示例：就地重新加密列

假定 SSN 列当前使用已启用 enclave 的列加密密钥（名为 CEK1）和确定性加密进行加密，在列级别设置的当前排序规则为 Latin1\_General\_BIN2，下面的语句将使用随机加密和相同密钥重新加密列。

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) COLLATE Latin1_General_BIN2
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1]
, ENCRYPTION_TYPE = Randomized
, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL;
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

假设 SSN 列当前是使用已启用 enclave 的列加密密钥 CEK1 和确定性加密进行加密，默认数据库排序规则是 BIN2 排序规则（尚未在列级别进行设置）。下面的语句使用已启用 enclave 的新密钥 CEK2 来重新加密列（无需更改加密类型）。

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) 
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK2]
, ENCRYPTION\_TYPE = Deterministic
, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL;
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

假设 SSN 列当前是使用已启用 enclave 的列加密密钥 CEK1 和确定性加密进行加密，默认数据库排序规则是 BIN2 排序规则（尚未在列级别进行设置）。下面的语句使用已启用 enclave 的新密钥和随机加密来重新加密列。 此外，在联机模式下执行此操作。

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) 
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1]
, ENCRYPTION_TYPE = Randomized
, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL 
WITH (ONLINE = ON);
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

### <a name="re-encrypt-columns-on-the-client-side"></a>在客户端重新加密列

重新加密（以及加密或解密）列的旧方法使用客户端工具，如 Always Encrypted 向导或 PowerShell。 一般情况下，不建议使用这种方法，除非包含（要重新加密的）列的表较小，且你的目标是将使用已启用 enclave 的新密钥重新加密列和更改加密类型（从确定性加密更改为随机加密）相结合。

如果重新加密使用随机加密的列，可能需要将它的排序规则更改为 BIN2 排序规则（在重新加密前后），才能解锁丰富计算。 请参阅“排序规则设置”部分了解详细信息。

有关详细信息，请参阅：

  - 使用 SSMS 轮替列加密密钥：<https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-wizard>
  - 使用 PowerShell 轮替列加密密钥：<https://docs.microsoft.com/sql/relational-databases/security/encryption/configure-column-encryption-using-powershell>

### <a name="decrypt-a-column-in-place"></a>就地解密列

如果使用已启用 enclave 的列加密密钥加密列，可以使用 ALTER TABLE 语句进行就地解密（转换为纯文本列）。 此外，在联机模式下执行此操作。

#### <a name="prerequisites-for-decrypting-a-column-in-place"></a>就地解密列的先决条件

- 使用已启用 enclave 的列加密密钥对列进行加密。
- 你有权访问列主密钥。

#### <a name="steps-for-decrypting-a-column-in-place"></a>就地解密列的步骤

1. 准备一个 SSMS 查询窗口，同时为数据库连接启用 Always Encrypted 和 enclave 计算。 有关详细信息，请参阅[准备一个启用了 Always Encrypted 的 SSMS 查询窗口](#prepare-an-ssms-query-window-with-always-encrypted-enabled)。

2. 在查询窗口中，发出带 ALTER COLUMN 子句的 [ALTER TABLE (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md) 语句，以便在没有  ENCRYPTED WITH 子句的情况下指定所需的列配置。
    
    > [!NOTE]
    > 如果列主密钥存储在 Azure Key Vault 中，系统可能会提示你登录到 Azure。

3. 清除访问表的所有批处理和存储过程的计划缓存，以刷新参数加密信息。 

    ```sql
    ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
    ```

    > [!NOTE]
    > 如果不从缓存中删除受影响的查询计划，加密后首次执行查询可能会失败。

    > [!NOTE]
    > 请谨慎使用 ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE 或 DBCC FREEPROCCACHE 来清除计划缓存，因为这可能会导致查询性能暂时降低。 若要使清除缓存的负面影响降到最低，可以选择性地仅删除受影响的查询计划。

4. 调用 [sp_refresh_parameter_encryption](../../system-stored-procedures/sp-refresh-parameter-encryption-transact-sql.md) 来更新每个模块（存储过程、函数、视图、触发器）的参数元数据，这些参数暂留在 [sys.parameters](../..//system-catalog-views/sys-parameters-transact-sql.md) 中，并且可能已通过解密列而失效。

#### <a name="example-for-decrypting-a-column-in-place"></a>示例：就地解密列

假定 SSN 列已加密，并且在列级设置的当前排序规则是 Latin1\_General\_BIN2，以下语句将解密列（并保持排序规则不变 - 或者，可以选择更改排序规则，例如，在同一语句中的更改为非 BIN2 排序规则）。

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) COLLATE Latin1_General_BIN2
WITH (ONLINE = ON);
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

## <a name="issue-rich-queries-against-encrypted-columns-using-ssms"></a>使用 SSMS 对加密列发出丰富查询

尝试对已启用 enclave 的列的丰富查询的最快方法是通过 SSMS 查询窗口，同时启用 Always Encrypted 参数化。 有关 SSMS 中此有用功能的详细信息，请参阅：

- [Always Encrypted 参数化 - 使用 SSMS 插入、更新和按加密列进行筛选](https://blogs.msdn.microsoft.com/sqlsecurity/2016/12/13/parameterization-for-always-encrypted-using-ssms-to-insert-into-update-and-filter-by-encrypted-columns/)
- [查询加密列](configure-always-encrypted-using-sql-server-management-studio.md#querying-encrypted-columns)

### <a name="prerequisites-for-issuing-rich-queries-against-encrypted-columns-using-ssms"></a>使用 SSMS 对加密列发出丰富查询的先决条件

- 要查询的列已启用 enclave。
- 你有权访问列主密钥（或密钥）。

### <a name="steps-for-issuing-rich-queries-against-encrypted-columns-using-ssms"></a>使用 SSMS 对加密列发出丰富查询的步骤

1. 准备一个 SSMS 查询窗口，同时为数据库连接启用 Always Encrypted 和 enclave 计算。 有关详细信息，请参阅[准备一个启用了 Always Encrypted 的 SSMS 查询窗口](#prepare-an-ssms-query-window-with-always-encrypted-enabled)。

2. 启用 Always Encrypted 参数化。

    1. 在 SSMS 的主菜单中，选择“查询”  。
    2. 选择“查询选项…”  。
    3. 导航到“执行”   > “高级”  。
    4. 选择或取消选择“启用 Always Encrypted 参数化”。
    5. 单击“确定”。

3. 在加密列上使用丰富计算创建和执行查询。 需要为面向查询中加密列的每个值声明 Transact-SQL 变量。 变量必须使用内联初始化（无法通过 SET 语句进行设置）。

    > [!NOTE]
    > 如果列主密钥存储在 Azure Key Vault 中，系统可能会提示你登录到 Azure。

### <a name="example-of-rich-queries-against-encrypted-columns"></a>示例：对加密列执行丰富查询

此示例假定数据库包含使用以下语句创建的表。

```sql
CREATE TABLE [dbo].[Employees]
(
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [SSN] [char](11) COLLATE Latin1_General_BIN2 ENCRYPTED WITH (
        COLUMN_ENCRYPTION_KEY = [CEK1],
        ENCRYPTION_TYPE = Randomized,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [Salary] [money] ENCRYPTED WITH (
        COLUMN_ENCRYPTION_KEY = [CEK1],
        ENCRYPTION_TYPE = Randomized,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
    CONSTRAINT [PK_dbo.Employees] PRIMARY KEY CLUSTERED (
[EmployeeID] ASC
)
) ON [PRIMARY];
GO
```

CEK1 是已启用 enclave 的列加密密钥。

以下是针对该表遵循参数化准则的查询示例：

```sql
DECLARE @SSNPattern [char](11) = '%1111%'
DECLARE @MinSalary [money] = 1000
SELECT *
FROM [dbo].[Employees]
WHERE SSN LIKE @SSNPattern
    AND [Salary] >= @MinSalary;
GO;
```

## <a name="create-and-use-indexes-on-enclave-enabled-columns-using-randomized-encryption"></a>在使用随机加密且已启用 enclave 的列上创建并使用索引

由于使用随机加密且已启用 enclave 的列上的索引会存储加密索引键值，而值是根据纯文本进行排序，因此 SQL Server 引擎必须将 enclave 用于任何涉及创建或更新索引的操作，包括：

- 创建或重新生成索引。
- 在包含索引列/加密列的表中插入、更新或删除行，这些操作触发向索引插入索引键和/或从索引中删除索引键。
- 运行涉及检查索引完整性的 DBCC 命令（例如，[DBCC CHECKDB (Transact-SQL)](../../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) 或 [DBCC CHECKTABLE (Transact-SQL)](../../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)）。
- 数据库恢复（例如，在 SQL Server 出现故障并重启后），前提是 SQL Server 需要撤消对索引的任何更改（如需了解更多详情，请参阅下文）。

以上所有操作都要求，enclave 必须包含索引列的列加密密钥，这样才能解密索引键。 通常情况下，enclave 可以通过下面两种方式之一获取列加密密钥：
- 直接从客户端应用程序获取。
- 从列加密密钥缓存获取。

### <a name="invoke-indexing-operations-with-column-encryption-keys-provided-directly-by-the-client"></a>使用客户端直接提供的列加密密钥调用索引操作

若要使用这种方法来调用索引操作，发出查询来对索引触发操作的应用程序必须：

- 连接到数据库，同时在数据库连接中同时启用 Always Encrypted 和 enclave 计算。
- 应用程序必须有权访问保护索引列的列加密密钥的列主密钥。

在 SQL Server 引擎分析应用程序查询，并确定需要更新加密列上的索引来执行查询后，它便会指示客户端驱动程序通过安全通道向 enclave 提供必需 CEK。 请注意，这与以下机制完全相同：向 enclave 提供列加密密钥，用于处理不涉及索引操作的查询。

这种方法可用于确保加密列上存在的索引对以下应用程序是透明的：已连接到数据库，同时已为连接启用 Always Encrypted 和 enclave 计算，并使用 enclave 处理查询。 当你在列上创建索引后，应用程序内的驱动程序便会以透明方式向 enclave 提供列加密密钥，以调用索引操作。 请注意，创建索引可能会增加需要查询数，这些查询要求应用程序必需向 enclave 发送列加密密钥。

有关如何使用这种方法的分步说明，请参阅[教程：在使用随机加密且已启用 enclave 的列上创建并使用索引。](../tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md)

### <a name="invoke-indexing-operations-using-cached-column-encryption-keys"></a>使用缓存列加密密钥调用索引操作

在客户端应用程序向 enclave 发送列加密密钥（以处理需要 enclave 计算的任意查询）后，enclave 便会将列加密密钥缓存在内部缓存（位于 enclave 内，无法从外部访问）中。

如果（相同或其他用户使用的）相同或其他客户端应用程序对索引触发操作，但未直接提供必需的列加密密钥，enclave 便会在缓存中查找列加密密钥。 这样一来，可以成功对索引触发操作，尽管客户端应用程序尚未提供密钥。

若要使用这种方法来调用索引操作，应用程序必须连接到数据库，但无需为连接启用 Always Encrypted，并且 enclave 内的缓存中必须有必需的列加密密钥。

只有无需使用列加密密钥来执行其他与索引无关的操作的查询，才支持使用这种方法来调用操作。 例如，如果应用程序使用 INSERT 语句将行插入包含加密列的表中，应用程序必须连接到数据库，同时在连接字符串中启用 Always Encrypted，并且必须有权访问键，无论加密列是否有索引。

这种方法可用于：

- 确保使用随机加密且已启用 enclave 的列上存在的索引对无权访问纯文本键和数据的应用程序和用户是透明的。 它确保在加密列上创建索引不会中断现有查询；也就是说，如果应用程序对包含加密列的表发出查询，而无需有权访问键，应用程序可以在 DBA 创建索引后继续运行，而无需有权访问键。 例如，假设当 DBA 在任意加密列上创建索引前，应用程序对上一示例中使用的“Employees”  表运行下面的查询。 

   ```sql
   DELETE FROM [dbo].[Employees] WHERE [EmployeeID] = 1;
   GO
   ```

   如果应用程序通过未启用 Always Encrypted 和 enclave 计算的连接提交查询，查询会成功，因为它未对加密列触发任何计算。 当 DBA 在任意加密列上创建索引后，查询便会触发从索引中删除索引键，而 enclave 需要列加密密钥来执行此操作。 不过，只要数据所有者已向 enclave 提供列加密密钥，应用程序就能够继续通过相同连接来运行此查询。

- 在管理索引时实现角色分隔，因为它启用 DBA 在加密列上创建并更改索引，而无需有权访问敏感数据。 

有关如何使用这种方法的分步说明，请参阅[教程：在使用随机加密且已启用 enclave 的列上创建并使用索引。](../tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md)

## <a name="develop-applications-issuing-rich-queries-in-visual-studio"></a>开发应用程序在 Visual Studio 中发出丰富查询

### <a name="set-up-your-visual-studio-project"></a>创建 Visual Studio 项目

若要在 .NET Framework 应用程序中使用具有安全 enclave 的 Always Encrypted，需要确保应用程序是针对 .NET Framework 4.7.2 生成的并与 [Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders NuGet](https://www.nuget.org/packages/Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders) 集成。 此外，如果将列主密钥中存储在 Azure Key Vault 中，还需要将应用程序与 [Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider NuGet](https://www.nuget.org/packages/Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider) 2.2.0 或更高版本集成。 

1. 打开 Visual Studio。
2. 创建新的 Visual C\# 项目，或打开现有项目。
3. 请确保项目至少面向 .NET Framework 4.7.2。 右键单击“解决方案资源管理器”中的项目，选择“属性”，将目标框架设置为“.NET Framework 4.7.2”。

4. 通过转到“工具”  （主菜单）>“NuGet 包管理器”   > “包管理器控制台”  安装以下 NuGet 包。 在“包管理器控制台”中运行以下代码。

   ```powershell
   Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders -IncludePrerelease
   ```

5. 如果使用 Azure Key Vault 来存储列主密钥，通过转到“工具”  （主菜单）>“NuGet 包管理器”   > “包管理器控制台”  安装以下 NuGet 包。 在“包管理器控制台”中运行以下代码。

   ```powershell
   Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider -IncludePrerelease -Version 2.2.0
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```

6. 选择项目并单击安装。
7. 从项目中打开配置文件（例如 App.config 或 Web.config）。
8. 找到 \<configuration\> 部分，并添加或更新 \<configSections\> 部分。

   A. 如果 \<configuration\> 部分不包含 \<configSections\> 部分，请直接在 \<configuration\> 下添加以下内容  。
   
      ```xml
      <configSections>
         <section name="SqlColumnEncryptionEnclaveProviders" type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
      </configSections>
      ```
   B. 如果 \<configruation\> 部分已包含 \<configSections\> 部分，请在 \<configSections\> 内添加以下行：

   ```xml
   <section name="SqlColumnEncryptionEnclaveProviders"  type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data,  Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" /\>
   ```

9. 在配置部分的 \<configSections\> 下添加以下部分，它指定一个 enclave 提供程序，用来证明并与 VBS enclave 进行交互：

   ```xml
   <SqlColumnEncryptionEnclaveProviders>
       <providers>
           <add name="VBS"  type="Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders.VirtualizationBasedSecurityEnclaveProvider,  Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders,    Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91"/>
       </providers>
   </SqlColumnEncryptionEnclaveProviders>
   ```

下面是一个简单控制台应用程序的 app.config 文件的完整示例。
```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <configSections>
    <section name="SqlColumnEncryptionEnclaveProviders" type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
  </configSections>
  <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.7.2" />
    </startup>

  <SqlColumnEncryptionEnclaveProviders>
    <providers>
      <add name="VBS" type="Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders.HostGuardianServiceEnclaveProvider, Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" />
    </providers>
  </SqlColumnEncryptionEnclaveProviders>
</configuration>
```
### <a name="develop-and-test-your-app"></a>开发和测试应用程序

若要使用 Always Encrypted 和 enclave 计算，应用程序必须连接到数据库，同时在连接字符串中使用以下两个关键字：`Column Encryption Setting = Enabled; Enclave Attestation Url=https://x.x.x.x/Attestation`（其中，xxxx 可以是 IP、域等）。

此外，应用程序需要遵循适用于使用 Always Encrypted 的应用程序的通用指导原则，例如，应用程序必须有权访问与应用程序查询中引用的数据库列相关联的列主密钥。

有关使用 Always Encrypted 开发 .NET Framework 应用程序的详细信息，请参阅以下文章：

- [配合使用 Always Encrypted 和 .NET Framework 数据提供程序进行开发](develop-using-always-encrypted-with-net-framework-data-provider.md)
- [Always Encrypted：保护 SQL 数据库中的敏感数据并将加密密钥存储在 Azure Key Vault 中](https://docs.microsoft.com/azure/sql-database/sql-database-always-encrypted)

#### <a name="example-of-simple-application"></a>简单应用程序示例

下面的代码是一个简单的 C\# 控制台应用程序示例，它使用以下架构发出针对表的 LIKE 查询：

```sql
CREATE TABLE [dbo].[Employees]
(
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [SSN] [char](11) ENCRYPTED WITH (
        COLUMN_ENCRYPTION_KEY = [CEK1],
        ENCRYPTION_TYPE = Randomized,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [Salary] [money] ENCRYPTED WITH (
        COLUMN_ENCRYPTION_KEY = [CEK1],
        ENCRYPTION_TYPE = Randomized,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
    CONSTRAINT [PK_dbo.Employees] PRIMARY KEY CLUSTERED (
[EmployeeID] ASC
)
) ON [PRIMARY];
GO
```

假定 CEK1 是已启用 enclave 的列加密密钥。

```cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Data.SqlClient;
using System.Data;
namespace ConsoleApp1
{
   class Program
   {
      static void Main(string\[\] args)
   {

   string connectionString = "Data Source = myserver; Initial Catalog = ContosoHR; Column Encryption Setting = Enabled;Enclave Attestation Url = https://10.193.16.185/Attestation/attestationservice.svc/signingCertificates; Integrated Security = true";

using (SqlConnection connection = new SqlConnection(connectionString))
{
   connection.Open();
   
   SqlCommand cmd = connection.CreateCommand();
   cmd.CommandText = @"SELECT [SSN], [FirstName], [LastName], [Salary] FROM [dbo].[Employees] WHERE [SSN] LIKE @SSNPattern AND [Salary] > @MinSalary;";
   
   SqlParameter paramSSNPattern = cmd.CreateParameter();
   
   paramSSNPattern.ParameterName = @"@SSNPattern";
   paramSSNPattern.DbType = DbType.AnsiStringFixedLength;
   paramSSNPattern.Direction = ParameterDirection.Input;
   paramSSNPattern.Value = "%1111";
   paramSSNPattern.Size = 11;
   
   cmd.Parameters.Add(paramSSNPattern);
   
   SqlParameter MinSalary = cmd.CreateParameter();
   
   MinSalary.ParameterName = @"@MinSalary";
   MinSalary.DbType = DbType.Currency;
   MinSalary.Direction = ParameterDirection.Input;
   MinSalary.Value = 900;
   
   cmd.Parameters.Add(MinSalary);
   cmd.ExecuteNonQuery();
   
   SqlDataReader reader = cmd.ExecuteReader();
   while (reader.Read())
   
   {
     Console.WriteLine(reader);
     Console.WriteLine(reader\[0\] + ", " + reader\[1\] + ", " + reader\[2\] + ", " + reader\[3\]);
   }

   Console.ReadKey();

   }
  }
 }
}
```
