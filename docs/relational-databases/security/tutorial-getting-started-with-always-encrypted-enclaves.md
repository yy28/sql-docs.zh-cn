---
title: 教程：通过 SSMS 开始使用具有安全 enclave 的 Always Encrypted | Microsoft Docs
ms.custom: ''
ms.date: 10/04/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: jaszymas
ms.author: jaszymas
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: c8c9e653781b821d3fcc2e7c2e5dd218b329e22c
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51675356"
---
# <a name="tutorial-getting-started-with-always-encrypted-with-secure-enclaves-using-ssms"></a>教程：通过 SSMS 开始使用具有安全 enclave 的 Always Encrypted
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本教程介绍如何开始使用[具有安全 enclave 的 Always Encrypted](encryption/always-encrypted-enclaves.md)。 它将介绍：
- 如何创建简单环境，以便测试和评估具有安全 enclave 的 Always Encrypted。
- 如何使用 SQL Server Management Studio (SSMS) 就地加密数据并就加密列发出各种查询。

## <a name="prerequisites"></a>必备条件

若要开始使用具有安全 enclave 的 Always Encrypted，需要至少两台计算机（可以是虚拟机）：

- SQL Server 计算机，用于承载 SQL Server 和 SSMS。
- HGS 计算机，用于运行 enclave 证明所需的主机保护者服务。

### <a name="sql-server-computer-requirements"></a>SQL Server 计算机要求

- [!INCLUDE [sssqlv15-md](../../includes/sssqlv15-md.md)] 或更高版本
- Windows 10 企业版 1809 或 Windows Server 2019 Datacenter
- [SQL Server Management Studio (SSMS) 18.0 或更高版](../../ssms/download-sql-server-management-studio-ssms.md)。

或者，可在另一台计算机上安装 SSMS。

>[!WARNING] 
>在生产环境中，切不可使用 SSMS 或其他工具来管理 Always Encrypted 密钥，或对 SQL Server 计算机上的加密数据运行查询，因为这将削弱或完全违背使用 Always Encrypted 的目的。

### <a name="hgs-computer-requirements"></a>HGS 计算机要求

- Windows Server 2019 Standard 或 Datacenter 版本
- 2 个 CPU
- 8 GB RAM
- 100 GB 存储

>[!NOTE]
>在开始之前，不应将 HGS 计算机加入域。

## <a name="step-1-configure-the-hgs-computer"></a>步骤 1：配置 HGS 计算机

在此步骤中，将配置 HGS 计算机，以运行支持主机密钥证明的主机保护者服务。

1. 以管理员身份（本地管理员）登录 HGS 计算机，打开提升的 Windows PowerShell 控制台并运行以下命令，添加主机保护者服务角色：

   ```powershell
   Install-WindowsFeature -Name HostGuardianServiceRole -IncludeManagementTools -Restart
   ```

2. 重启 HGS 计算机后，再次使用管理员帐户登录，打开提升的 Windows PowerShell 控制台并运行以下命令，安装主机保护者服务并配置它的域。 此处指定的密码仅适用于 Active Directory 的目录服务修复模式密码，而不会更改管理员帐户的登录密码。 可以为 -HgsDomainName 提供所选的任何域名。

   ```powershell
   $adminPassword = ConvertTo-SecureString -AsPlainText '<password>' -Force
   Install-HgsServer -HgsDomainName 'bastion.local' -SafeModeAdministratorPassword $adminPassword -Restart
   ```

3. 再次重启计算机后，使用管理员帐户（现在也是域管理员）登录，打开提升的 Windows PowerShell 控制台，配置 HGS 实例的主机密钥证明。 

   ```powershell
   Initialize-HgsAttestation -HgsServiceName 'hgs' -TrustHostKey  
   ```

4. 运行以下命令，找到 HGS 计算机的 IP 地址。 保存此 IP 地址，以供后续步骤使用。

   ```powershell
   Get-NetIPAddress  
   ```

>[!NOTE]
>或者，如果想通过 DNS 名称来引用 HGS 计算机，可设置一个转发器，从公司 DNS 服务器指向新的 HGS 域控制器。  

## <a name="step-2-configure-the-sql-server-computer-as-a-guarded-host"></a>步骤 2：将 SQL Server 计算机配置为受保护的主机
在此步骤中，需将 SQL Server 计算机配置为受保护的主机，并使用主机密钥证明向 HGS 注册。
>[!NOTE]
>建议仅在测试环境中使用主机密钥证明。 对于生产环境，应使用 TPM 证明。

1. 以管理员身份登录 SQL Server，打开提升的 Windows PowerShell 控制台，安装受保护的主机功能，此操作还将同时安装 Hyper-V（如果尚未安装）。

   ```powershell
   Enable-WindowsOptionalFeature -Online -FeatureName HostGuardian -All
   ```

2. 系统提示 Hyper-V 安装完成时，请重启 SQL Server 计算机。
3. 检索以下变量的值，确定 SQL Server 计算机的名称。

   ```powershell
   $env:computername 
   ```

4. 再次以管理员身份登录 SQL Server 计算机，打开提升的 Windows PowerShell 控制台，生成唯一主机密钥，并将生成的公钥导出到文件。

   ```powershell
   Set-HgsClientHostKey 
   Get-HgsClientHostKey -Path $HOME\Desktop\hostkey.cer
   ```

5. 将上一步生成的主机密钥文件复制到 HGS 计算机。 以下说明假定文件名为 hostkey.cer 并且计划将其复制到 HGS 计算机的桌面。
6. 在 HGS 计算机上，打开提升的 Windows PowerShell 控制台并向 HGS 注册 SQL Server 计算机的主机密钥：

   ```powershell
   Add-HgsAttestationHostKey -Name <your SQL Server computer name> -Path $HOME\Desktop\hostkey.cer
   ```

7. 在 SQL Server 计算机上，在提升的 Windows PowerShell 控制台中运行以下命令，告诉 SQL Server 计算机前往何处进行证明。 请确保已指定 HGS 计算机的 IP 地址或 DNS 名称。 

   ```powershell
   Set-HgsClientConfiguration -AttestationServerUrl https://<IP address or DNS name>/Attestation -KeyProtectionServerUrl https://<IP address or DNS name>/KeyProtection/  
   ```

上述命令的结果应显示 AttestationStatus = Passed。

如果出现 HostUnreachable 错误，这意味着 SQL Server 计算机无法与 HGS 通信。 请确保可以连接到 HGS 计算机。

UnauthorizedHost 错误表示公钥未向 HGS 服务器注册，请重复步骤 5 和 6 以解决该错误。

如果所有其他方法均失败，请运行 Clear-HgsClientHostKey 并重复步骤 4-7。

## <a name="step-3-enable-always-encrypted-with-secure-enclaves-in-sql-server"></a>步骤 3：在 SQL Server 中启用具有安全 enclave 的 Always Encrypted

在此步骤中，将在 SQL Server 实例中启用使用 enclave 的 Always Encrypted 功能。

1. 打开 SSMS，以系统管理员身份连接到 SQL Server 实例，并打开新的查询窗口。
2. 将安全 enclave 类型配置为 VBS。

   ```sql
   EXEC sys.sp_configure 'column encryption enclave type', 1
   RECONFIGURE
   ```

3. 重启 SQL Server 实例，前述更改才会生效。 可在“对象资源管理器”中右键单击实例并选择“重启”，从而在 SSMS 中重启实例。 重启实例后，请重新连接到它。

4. 通过运行以下查询确认现已加载安全 enclave：

   ```sql
   SELECT [name], [value], [value_in_use] FROM sys.configurations
   WHERE [name] = 'column encryption enclave type'
   ```

    查询应返回类似于以下的行：  

    | NAME                           | 值 | value_in_use |
    | ------------------------------ | ----- | -------------- |
    | 列加密 enclave 类型 | 1     | 1              |

5. 若要启用对加密列的大量计算，请运行以下查询：

   ```sql
   DBCC traceon(127,-1)
   ```

    > [!NOTE]
    > 默认情况下，[!INCLUDE [sssqlv15-md](../../includes/sssqlv15-md.md)] 中禁用了大量计算。 每次重启 SQL Server 实例之后，都需要使用上述语句启用它们。

## <a name="step-4-create-a-sample-database"></a>步骤 4：创建示例数据库
在此步骤中，将创建包含一些示例数据的数据库，稍后将对其进行加密。

1. 使用 SSMS 连接到 SQL Server 实例。
2. 创建名为 ContosoHR 的新数据库。

    ```sql
    CREATE DATABASE [ContosoHR] COLLATE Latin1_General_BIN2
    ```

3. 确保已连接到新建的数据库。 创建名为“员工”的新表。

    ```sql
    CREATE TABLE [dbo].[Employees]
    (
        [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
        [SSN] [char](11) NOT NULL,
        [FirstName] [nvarchar](50) NOT NULL,
        [LastName] [nvarchar](50) NOT NULL,
        [Salary] [money] NOT NULL
    ) ON [PRIMARY]
    GO
    ```

4. 向“员工”表添加多条员工记录。

    ```sql
    INSERT INTO [dbo].[Employees]
            ([SSN]
            ,[FirstName]
            ,[LastName]
            ,[Salary])
        VALUES
            ('795-73-9838'
            , N'Catherine'
            , N'Abel'
            , $31692)
    GO

    INSERT INTO [dbo].[Employees]
            ([SSN]
            ,[FirstName]
            ,[LastName]
            ,[Salary])
        VALUES
            ('990-00-6818'
            , N'Kim'
            , N'Abercrombie'
            , $55415)
    GO
    ```

## <a name="step-5-provision-enclave-enabled-keys"></a>步骤 5：预配已启用 enclave 的密钥

在此步骤中，将创建允许 enclave 计算的列主密钥和列加密密钥。

1. 使用 SSMS 连接到你的数据库。
2. 在“对象资源管理器”中，展开数据库，然后导航到“安全” > “Always Encrypted 密钥”。
3. 预配已启用 enclave 的新列主密钥：
    1. 右键单击“Always Encrypted 密钥”，然后选择“新列主密钥...”。
    2. 选择列主密钥名称：CMK1。
    3. 请确保选择“Windows 证书存储(当前用户或本地计算机)”或“Azure Key Vault”。
    4. 选择“允许 enclave 计算”。
    5. 如果选择了 Azure Key Vault，请登录到 Azure 并选择密钥保管库。 若要深入了解如何创建 Always Encrypted 的密钥保管库，请参阅 [Manage your key vaults from Azure portal](https://blogs.technet.microsoft.com/kv/2016/09/12/manage-your-key-vaults-from-new-azure-portal/)（从 Azure 门户管理密钥保管库）。
    6. 如已存在，则请选择密钥，或按照窗体上的说明创建新密钥。
    7. 选择“确定”。

        ![允许 enclave 计算](encryption/media/always-encrypted-enclaves/allow-enclave-computations.png)

4. 创建已启用 enclave 的新列加密密钥：

    1. 右键单击“Always Encrypted 密钥”，然后选择“新建列加密密钥”。
    2. 输入新列加密密钥的名称：CEK1。
    3. 在“列主密匙”下拉列表中，选择在上一步骤创建的列主密钥。
    4. 选择“确定”。

## <a name="step-6-encrypt-some-columns-in-place"></a>步骤 6：就地加密位部分列

在此步骤中，将加密存储在服务器端 enclave 内 SSN 和“工资”列中的数据，然后对数据进行 SELECT 查询测试。

1. 在 SSMS 中，为数据库连接配置启用了 Always Encrypted 的查询窗口。
    1. 在 SSMS 中，打开一个新的查询窗口。
    2. 右键单击新查询窗口中的任意位置。
    3. 选择“连接”\>“更改连接”。
    4. 选择“选项”。 导航到“Always Encrypted”选项卡，选择“启用 Always Encrypted”，然后指定 enclave 证明 URL。
    5. 选择“连接”。
2. 在 SSMS 中，为数据库连接配置另一个禁用了 Always Encrypted 的查询窗口。
    1. 在 SSMS 中，打开一个新的查询窗口。
    2. 右键单击新查询窗口中的任意位置。
    3. 选择“连接”\>“更改连接”。
    4. 选择“选项”。 导航到“Always Encrypted”选项卡，请确保未选中“启用 Always Encrypted”。
    5. 选择“连接”。
3. 加密 SSN 和“工资”列。 在启用了 Always Encrypted 的查询窗口中，粘贴并执行以下语句：

    ```sql
    ALTER TABLE [dbo].[Employees]
    ALTER COLUMN [SSN] [char] (11)
    ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
    WITH
    (ONLINE = ON)
    GO
    DBCC FREEPROCCACHE
    GO

    ALTER TABLE [dbo].[Employees]
    ALTER COLUMN [Salary] [money]
    ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
    WITH
    (ONLINE = ON)
    GO
    DBCC FREEPROCCACHE
    GO
    ```

4. 若要验证 SSN 和“工资”列现在是否已加密，请在禁用了 Always Encrypted 的查询窗口中，粘贴并执行以下语句。 查询窗口应返回 SSN 和“工资”列中的加密值。 在启用了 Always Encrypted 的查询窗口中尝试执行同一查询，查看解密数据。

    ```sql
    SELECT * FROM [dbo].[Employees]
    ```

## <a name="step-7-run-rich-queries-against-encrypted-columns"></a>步骤 7：对加密列运行丰富查询

现在，可对加密列运行丰富查询。 部分查询处理将在服务器端 enclave 内执行。 

1. 启用 Always Encrypted 参数化。
    1. 在 SSMS 的主菜单中，选择“查询”。
    2. 选择“查询选项…” 。
    3. 导航到“执行” > “高级”。
    4. 选择或取消选择“启用 Always Encrypted 参数化”。
    5. 选择“确定”。
2. 在启用了 Always Encrypted 的查询窗口中，粘贴并执行以下查询。 该查询应返回满足指定搜索条件的纯文本值和行。

    ```sql
    DECLARE @SSNPattern [char](11) = '%6818'
    DECLARE @MinSalary [money] = $1000
    SELECT * FROM [dbo].[Employees]
    WHERE SSN LIKE @SSNPattern AND [Salary] >= @MinSalary;
    ```

## <a name="next-steps"></a>Next Steps
请参阅[配置具有安全 enclave 的 Always Encrypted](encryption/configure-always-encrypted-enclaves.md)，了解其他用例。 此外，还可以进行以下尝试：

- [配置 TPM 证明。](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-initialize-hgs-tpm-mode)
- [为 HGS 实例配置 HTTPS。](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-configure-hgs-https)
- 开发对加密列发出丰富查询的应用程序。
