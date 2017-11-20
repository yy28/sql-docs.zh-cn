---
title: "部署、 运行和监视在 Azure 上的 SSIS 包 |Microsoft 文档"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: lift-shift
ms.suite: sql
ms.custom: 
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 560965a241b24a09f50a23faf63ce74d0049d5a7
ms.openlocfilehash: 2e16666c412870cc55024e7156752f43ddbc1800
ms.contentlocale: zh-cn
ms.lasthandoff: 10/13/2017

---
# <a name="deploy-run-and-monitor-an-ssis-package-on-azure"></a>部署、 运行和监视在 Azure 上的 SSIS 包
本教程演示如何将 SQL Server Integration Services 项目部署到 Azure SQL 数据库上的 SSISDB 目录数据库、 Azure SSIS 集成运行库，在运行包和监视正在运行的包。

## <a name="prerequisites"></a>先决条件

在开始之前，请确保您有 17.2 或更高版本的 SQL Server Management Studio 版本。 若要下载最新版本的 SSMS，请参阅[下载 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。

此外请确保你已将 SSISDB 数据库设置并设置 Azure SSIS 集成运行库。 有关如何设置 Azure 上的 SSIS 的信息，请参阅[提起并移动到 Azure 包 SQL Server Integration Services (SSIS)](https://docs.microsoft.com/en-us/azure/data-factory/tutorial-deploy-ssis-packages-azure)。

## <a name="connect-to-the-ssisdb-database"></a>连接到 SSISDB 数据库

使用 SQL Server Management Studio 连接到你的 Azure SQL 数据库服务器上的 SSIS 目录。 有关详细信息，请参阅[连接到 Azure 上的 SSISDB 目录数据库](ssis-azure-connect-to-catalog-database.md)。

> [!IMPORTANT]
> Azure SQL 数据库服务器在端口 1433年上侦听。 如果你正在尝试连接到 Azure SQL 数据库服务器从企业防火墙内，此端口必须为你成功连接到企业防火墙中打开。

1. 打开 SQL Server Management Studio。

2. **连接到服务器**。 在**连接到服务器**对话框框中，输入以下信息：

   | 设置       | 建议的值 | Description | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **服务器类型** | 数据库引擎 | 此值是必需的。 |
   | **服务器名称** | 完全限定的服务器名称 | 名称应为按以下格式： **mysqldbserver.database.windows.net**。 如果你需要服务器名称，请参阅[连接到 Azure 上的 SSISDB 目录数据库](ssis-azure-connect-to-catalog-database.md)。 |
   | **身份验证** | SQL Server 身份验证 | 此快速开始使用 SQL 身份验证。 |
   | **登录** | 与服务器管理员帐户 | 这是你在创建服务器时指定的帐户。 |
   | **密码** | 你的服务器管理员帐户的密码 | 这是你在创建服务器时指定的密码。 |

3. **连接到 SSISDB 数据库**。 选择**选项**以展开**连接到服务器**对话框。 在展开**连接到服务器**对话框中，选择**连接属性**选项卡。在**连接到数据库**字段中，选择或输入`SSISDB`。

4. 然后选择**连接**。 在 SSMS 中打开对象资源管理器窗口。 

5. 在对象资源管理器，展开**Integration Services 目录**然后展开**SSISDB** SSIS 目录数据库中查看的对象。

## <a name="deploy-a-project"></a>部署项目

### <a name="start-the-integration-services-deployment-wizard"></a>启动 Integration Services 部署向导
1. 在对象资源管理器在 SSMS 中，与**Integration Services 目录**节点和**SSISDB**已展开的节点，展开项目文件夹。

2.  选择**项目**节点。

3.  右键单击**项目**节点，然后选择**部署项目**。 Integration Services 部署向导将打开。 你可以部署的项目从 SSIS 目录数据库或从文件系统。

### <a name="deploy-a-project-with-the-deployment-wizard"></a>部署项目部署向导
1. 上**简介**页的部署向导中，查看简介。 选择**下一步**以打开**选择源**页。

2. 上**选择源**页上，选择要部署的现有 SSIS 项目。
    -   若要部署你所创建的项目部署文件，请选择“项目部署文件”  并输入 .ispac 文件的路径。
    -   若要部署的 SSIS 目录中驻留的项目，选择**Integration Services 目录**，，然后输入服务器名称和路径的目录中的项目。
    -   选择**下一步**若要查看**选择目标**页。
  
3.  上**选择目标**页上，选择项目的目标。
    -   输入完全限定的服务器名称格式`<server_name>.database.windows.net`。
    -   然后选择**浏览**在 SSISDB 中选择目标文件夹。
    -   选择**下一步**以打开**评审**页。  
  
4.  上**查看**页上，查看所选的设置。
    -   你可以通过选择更改你的选择**上一步**，或通过在左窗格中选择的任何步骤。
    -   选择**部署**来启动部署过程。
  
5.  在部署过程完成后**结果**页将打开。 该页显示每个操作是成功了还是失败了。
    -   如果操作失败，则选择**失败**中**结果**列以显示的错误说明。
    -   （可选） 选择**保存报表...**将结果保存到 XML 文件。
    -   选择**关闭**以退出向导。

## <a name="run-a-package"></a>运行包

1. 在对象资源管理器在 SSMS 中，选择你想要运行的包。

2. 右键单击并选择**执行**以打开**执行包**对话框。

3.  在**执行包**对话框框中，通过使用上的设置来配置包执行**参数**，**连接管理器**，和**高级**选项卡。

4.  选择**确定**运行包。

## <a name="monitor-the-running-package-in-ssms"></a>监视在 SSMS 中正在运行的包

若要查看当前运行在 Integration Services 服务器上，例如部署、 验证和包执行的 Integration Services 操作的状态使用**活动操作**在 SSMS 中的对话框。 若要打开**活动操作**对话框中，右键单击**SSISDB**，然后选择**活动操作**。

也可以在对象资源管理器，右键单击并选择中选择包**报表**，然后**标准报表**，然后**所有执行**。

有关如何监视正在运行的包，在 SSMS 中的详细信息，请参阅[监视器正在运行的包和其他操作](https://docs.microsoft.com/en-us/sql/integration-services/performance/monitor-running-packages-and-other-operations)。

## <a name="monitor-the-azure-ssis-integration-runtime"></a>监视 Azure SSIS 集成运行库

若要获取有关 Azure SSIS 集成运行库在运行包的状态信息，请使用以下 PowerShell 命令： 对于每个命令提供的数据工厂、 Azure SSIS IR，和资源组的名称。

### <a name="get-metadata-about-the-azure-ssis-integration-runtime"></a>获取有关 Azure SSIS 集成运行时元数据

```powershell
Get-AzureRmDataFactoryV2IntegrationRuntime -DataFactoryName $DataFactoryName -Name $AzureSsisIRName -ResourceGroupName $ResourceGroupName
```

### <a name="get-the-status-of-the-azure-ssis-integration-runtime"></a>获取 Azure SSIS 集成运行库的状态

```powershell
Get-AzureRmDataFactoryV2IntegrationRuntime -Status -DataFactoryName $DataFactoryName -Name $AzureSsisIRName -ResourceGroupName $ResourceGroupName
```

## <a name="next-steps"></a>后续步骤
- 了解如何安排软件包执行。 有关详细信息，请参阅[计划 SSIS 包在 Azure 上的执行](ssis-azure-schedule-packages.md)

