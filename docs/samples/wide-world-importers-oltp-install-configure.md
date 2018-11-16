---
title: 安装和配置 WideWorldImporters 示例数据库-SQL |Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c31c6c2071d276da9b3ab0e498a090659ba589a7
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51673476"
---
# <a name="installation-and-configuration"></a>安装和配置
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Wide World Importers OLTP 数据库安装和配置说明。

## <a name="prerequisites"></a>必要條件

- [SQL Server 2016](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) （或更高版本） 或[Azure SQL 数据库](https://azure.microsoft.com/services/sql-database/)。 对于该示例的完整版本，使用 SQL Server 评估/开发人员/企业版。
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)。 为获得最佳结果使用 2016 年 6 月发行版或更高版本。

## <a name="download"></a>下载

该示例的最新版本：

[wide-world-importers-release](https://go.microsoft.com/fwlink/?LinkID=800630)

将示例 WideWorldImporters 数据库备份/bacpac 下载对应到你的 SQL Server 或 Azure SQL 数据库版本。

从以下位置提供了源代码以重新创建示例数据库。 请注意因为有处于数据生成一个随机因子，重新创建该示例会导致数据，略有差异：

[wide-world-importers](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-database-scripts)

## <a name="install"></a>Install


### <a name="sql-server"></a>SQL Server

若要将备份还原到 SQL Server 实例，可以使用 Management Studio。

1. 打开 SQL Server Management Studio 并连接到目标 SQL Server 实例。
2. 右键单击**数据库**节点，然后选择**Restore Database**。
3. 选择**设备**，然后单击按钮 **...**
4. 在对话框**选择备份设备**，单击**添加**，导航到的服务器的文件系统中的数据库备份，并选择的备份。 单击“确定” 。
5. 如果需要更改数据的目标位置，并在日志文件，**文件**窗格。 请注意，它将数据和日志文件的不同驱动器上的最佳做法。
6. 单击“确定” 。 这将启动数据库还原。 完成后，您将拥有数据库安装在您的 SQL Server 实例上的 WideWorldImporters。

### <a name="azure-sql-database"></a>Azure SQL Database

将 bacpac 导入新的 SQL 数据库，可以使用 Management Studio。

1. （可选）如果你还没有 SQL Server 在 Azure 中，导航到[Azure 门户](https://portal.azure.com/)并创建新的 SQL 数据库。 过程中创建数据库，将创建的服务器。 记下的服务器。
   - 请参阅[本教程](https://azure.microsoft.com/documentation/articles/sql-database-get-started/)在几分钟内创建数据库
2. 打开 SQL Server Management Studio 并连接到 Azure 中的服务器。
3. 右键单击**数据库**节点，然后选择**导入数据层应用程序**。
4. 在中**导入设置**选择**从本地磁盘导入**和选择示例数据库的 bacpac 从您的文件系统。
5. 下**数据库设置**更改到的数据库名称*WideWorldImporters*和选择要使用的目标版本和服务目标。
6. 单击**下一步**并**完成**开始部署。 它将 P1 上完成几分钟时间。 如果较低的定价层是所需的我们建议新的 P1 数据库，导入，然后将定价层更改为所需的级别。

## <a name="configuration"></a>配置

### <a name="full-text-indexing"></a>全文索引

示例数据库可以使用全文索引。 但是，与 SQL Server 的默认情况下不安装该功能-你需要在 SQL Server 安装程序 （Azure SQL DB 中的默认情况下已启用） 过程中选择它。 因此，安装后步骤是必需的。

1. 在 SQL Server Management Studio，连接到 WideWorldImporters 数据库并打开新查询窗口。
2. 运行以下 T-SQL 命令，以便在数据库中的全文索引使用：  `EXECUTE Application.Configuration_ApplyFullTextIndexing`


### <a name="sql-server-audit"></a>SQL Server 审核

适用范围： SQL Server

启用 SQL Server 中的审核要求服务器配置。 若要启用 SQL Server 审核 WideWorldImporters 示例，请在数据库中运行以下语句：

    EXECUTE [Application].[Configuration_ApplyAuditing]

在 Azure SQL 数据库审核配置通过[Azure 门户](https://portal.azure.com/)。

### <a name="row-level-security"></a>行级安全性

适用于： Azure SQL 数据库

WideWorldImporters 的 bacpac 下载中默认情况下不启用行级别安全性。 若要在数据库中启用行级别安全性，请运行以下存储的过程：

    EXECUTE [Application].[Configuration_ApplyRowLevelSecurity]

