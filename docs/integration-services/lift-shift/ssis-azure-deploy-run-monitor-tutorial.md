---
title: 在 Azure 中部署和运行 SSIS 包 | Microsoft Docs
ms.date: 02/05/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.component: lift-shift
ms.suite: sql
ms.custom: ''
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 27c7e77b5143bca56b7ded2233c01e11ad088d5f
ms.sourcegitcommit: 0cc2cb281e467a13a76174e0d9afbdcf4ccddc29
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2018
---
# <a name="deploy-and-run-an-ssis-package-in-azure"></a>在 Azure 中部署和运行 SSIS 包
本教程演示如何将 SQL Server Integration Services 项目部署到 Azure SQL 数据库上的 SSISDB 目录数据库、在 Azure-SSIS Integration Runtime 中运行包，以及监视正在运行的包。

## <a name="prerequisites"></a>必备条件

开始之前，请确保有 SQL Server Management Studio 版本 17.2 或更高版本。 若要下载 SSMS 最新版本，请参阅[下载 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。

另外确保已经设置 SSISDB 数据库并预配 Azure-SSIS Integration Runtime。 有关如何在 Azure 上预配 SSIS 的信息，请参阅[将 SSIS 包部署到 Azure](https://docs.microsoft.com/azure/data-factory/tutorial-create-azure-ssis-runtime-portal)。

> [!NOTE]
> 若要部署到 Azure，只能使用项目部署模型。

## <a name="connect-to-the-ssisdb-database"></a>连接到 SSISDB 数据库

使用 SQL Server Management Studio 连接到 Azure SQL 数据库服务器上的 SSIS 目录。 有关详细信息和屏幕截图，请参阅[连接到 Azure 上的 SSISDB 目录数据库](ssis-azure-connect-to-catalog-database.md)。

请务必注意下面最重要的两点。 有关具体步骤，请参阅以下过程。
-   采用格式“mysqldbserver.database.windows.net”，输入 Azure SQL 数据库服务器的完全限定的名称。
-   选择 `SSISDB` 数据库以供连接。

> [!IMPORTANT]
> Azure SQL 数据库服务器侦听端口 1433。 如果尝试从企业防火墙内连接到 Azure SQL 数据库服务器，必须在企业防火墙中打开该端口，才能成功连接。

1. 打开 SQL Server Management Studio。

2. **连接到该服务器**。 在“连接到服务器”对话框中，输入以下信息：

   | 设置       | 建议的值 | 描述 | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **服务器类型** | 数据库引擎 | 此值是必需的。 |
   | **服务器名称** | 完全限定的服务器名称 | 名称应采用此格式：**mysqldbserver.database.windows.net**。 如果需要服务器名称，请参阅[连接到 Azure 上的 SSISDB 目录数据库](ssis-azure-connect-to-catalog-database.md)。 |
   | **身份验证** | SQL Server 身份验证 | 本快速入门使用 SQL 身份验证。 |
   | **登录** | 服务器管理员帐户 | 在创建服务器时指定的帐户。 |
   | **密码** | 服务器管理员帐户的密码 | 在创建服务器时指定的密码。 |

3. **连接到 SSISDB 数据库**。 选择“选项”展开“连接到服务器”对话框。 在展开的“连接到服务器”对话框中，选择“连接属性”选项卡。在“连接到数据库”字段中，选择或输入 `SSISDB`。

4. 然后选择“连接”。 对象资源管理器窗口随即在 SSMS 中打开。 

5. 在对象资源管理器中，展开“Integration Services 目录”，然后展开“SSISDB”，查看 SSIS 目录数据库中的对象。

## <a name="deploy-a-project-with-the-deployment-wizard"></a>使用部署向导部署项目

若要详细了解如何部署包和部署向导，请参阅[部署 Integration Services (SSIS) 项目和包](../packages/deploy-integration-services-ssis-projects-and-packages.md)和 [Integration Services 部署向导](../packages/deploy-integration-services-ssis-projects-and-packages.md#integration-services-deployment-wizard)。

### <a name="start-the-integration-services-deployment-wizard"></a>启动 Integration Services 部署向导
1. 在 SSMS 的对象资源管理器中，在展开“Integration Services 目录”节点和“SSISDB”节点后，展开一个项目文件夹。

2.  选择“项目”节点。

3.  右键单击“项目”节点，选择“部署项目”。 Integration Services 部署向导随即打开。 可以从 SSIS 目录数据库或从文件系统部署项目。

    ![通过 SSMS 部署项目](media/ssis-azure-deploy-run-monitor-tutorial/ssisdb-deploy-project1.png)

    ![此时，SSIS 部署向导对话框打开](media/ssis-azure-deploy-run-monitor-tutorial/ssisdb-deploy-project2.png)

### <a name="deploy-a-project-with-the-deployment-wizard"></a>使用部署向导部署项目
1. 在部署向导的“简介”页上查看简介。 选择“下一步”打开“选择源”页。

2. 在“选择源”页上，选择要部署的现有 SSIS 项目。
    -   若要部署你所创建的项目部署文件，请选择“项目部署文件”  并输入 .ispac 文件的路径。
    -   若要部署位于 SSIS 目录中的项目，请选择“Integration Services 目录”，然后输入目录中该项目的服务器名称和路径。
    -   选择“下一步”查看“选择目标”页。
  
3.  在“选择目标”页上，选择项目目标。
    -   使用 `<server_name>.database.windows.net` 格式输入完全限定服务器名称。
    -   然后选择“浏览”，在 SSISDB 中选择目标文件夹。
    -   选择“下一步”打开“查看”页。  
  
4.  在“查看”页上，查看所选的设置。
    -   可以通过选择“上一步”或选择左窗格中的任意步骤来更改所做的选择。
    -   选择“部署”启动部署过程。

    > ![注意] 如果收到错误消息“没有任何活动工作代理。(.Net SqlClient 数据提供程序)”，请确保 Azure SSIS Integration Runtime 正在运行。 如果尝试在 Azure SSIS IR 处于停止状态时进行部署，则会发生此错误。

5.  部署过程完成之后，“结果”页随即打开。 该页显示每个操作是成功了还是失败了。
    -   如果操作失败，则选择“结果”列中的“失败”以显示错误说明。
    -   （可选）选择“保存报告...”将结果保存到 XML 文件中。
    -   选择“关闭”退出该向导。

## <a name="deploy-a-project-with-powershell"></a>使用 PowerShell 部署项目

若要使用 PowerShell 将项目部署到 Azure SQL 数据库上的 SSISDB，请根据具体要求修改以下脚本。 此脚本枚举了 `$ProjectFilePath` 下的子文件夹以及每个子文件夹中的项目，然后在 SSISDB 中创建相同的文件夹，并将项目部署到这些文件夹。

此脚本要求在运行脚本的计算机上安装 SQL Server Data Tools 版本 17.x 或 SQL Server Management Studio。

```powershell
# Variables
$ProjectFilePath = "C:\<folder>"
$SSISDBServerEndpoint = "<servername>.database.windows.net"
$SSISDBServerAdminUserName = "<username>"
$SSISDBServerAdminPassword = "<password>"

# Load the IntegrationServices Assembly
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.Management.IntegrationServices") | Out-Null;

# Store the IntegrationServices Assembly namespace to avoid typing it every time
$ISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"

Write-Host "Connecting to server ..."

# Create a connection to the server
$sqlConnectionString = "Data Source=" + $SSISDBServerEndpoint + ";User ID="+ $SSISDBServerAdminUserName +";Password="+ $SSISDBServerAdminPassword + ";Initial Catalog=SSISDB"
$sqlConnection = New-Object System.Data.SqlClient.SqlConnection $sqlConnectionString

# Create the Integration Services object
$integrationServices = New-Object $ISNamespace".IntegrationServices" $sqlConnection

# Get the catalog
$catalog = $integrationServices.Catalogs['SSISDB']

write-host "Enumerating all folders..."

$folders = ls -Path $ProjectFilePath -Directory

if ($folders.Count -gt 0)
{
    foreach ($filefolder in $folders)
    {
        Write-Host "Creating Folder " $filefolder.Name " ..."

        # Create a new folder
        $folder = New-Object $ISNamespace".CatalogFolder" ($catalog, $filefolder.Name, "Folder description")
        $folder.Create()

        $projects = ls -Path $filefolder.FullName -File -Filter *.ispac
        if ($projects.Count -gt 0)
        {
            foreach($projectfile in $projects)
            {
                $projectfilename = $projectfile.Name.Replace(".ispac", "")
                Write-Host "Deploying " $projectfilename " project ..."

                # Read the project file, and deploy it to the folder
                [byte[]] $projectFileContent = [System.IO.File]::ReadAllBytes($projectfile.FullName)
                $folder.DeployProject($projectfilename, $projectFileContent)
            }
        }
    }
}

Write-Host "All done." 
```

## <a name="run-a-package"></a>运行包

1. 在 SSMS 的对象资源管理器中，选择要运行的包。

2. 右击并选择“执行”打开“执行包”对话框。

3.  在“执行包”对话框中，使用“参数”、“连接管理器”和“高级”选项卡上的设置来配置包执行。

4.  选择“确定”运行包。

## <a name="monitor-the-running-package-in-ssms"></a>在 SSMS 中监视正在运行的包

若要查看 Integration Services 服务器上当前运行的 Integration Services 操作的状态，比如部署、验证和包执行，请使用 SSMS 中的“活动操作”对话框。 若要打开“活动操作”对话框，请右键单击“SSISDB”，然后选择“活动操作”。

也可以在对象资源管理器中选择包，右击并选择“报表”，然后选择“标准报表”、“所有执行”。

有关如何在 SSMS 中监视正在运行的包的详细信息，请参阅[监视正在运行的包和其他操作](https://docs.microsoft.com/sql/integration-services/performance/monitor-running-packages-and-other-operations)。

## <a name="monitor-the-azure-ssis-integration-runtime"></a>监视 Azure-SSIS Integration Runtime

若要获取有关正在运行包的 Azure-SSIS Integration Runtime 的状态信息，请使用以下 PowerShell 命令：对于每个命令，均提供数据工厂、Azure-SSIS IR 和资源组的名称。

### <a name="get-metadata-about-the-azure-ssis-integration-runtime"></a>获取有关 Azure-SSIS Integration Runtime 的元数据

```powershell
Get-AzureRmDataFactoryV2IntegrationRuntime -DataFactoryName $DataFactoryName -Name $AzureSsisIRName -ResourceGroupName $ResourceGroupName
```

### <a name="get-the-status-of-the-azure-ssis-integration-runtime"></a>获取 Azure-SSIS Integration Runtime 的状态

```powershell
Get-AzureRmDataFactoryV2IntegrationRuntime -Status -DataFactoryName $DataFactoryName -Name $AzureSsisIRName -ResourceGroupName $ResourceGroupName
```

## <a name="next-steps"></a>后续步骤
- 了解如何计划包执行。 有关详细信息，请参阅[计划 Azure 上的 SSIS 包执行](ssis-azure-schedule-packages.md)
