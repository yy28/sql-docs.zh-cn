---
title: "安装和配置 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: samples
ms.technology: samples
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6dd1f09b-dcff-4627-899a-eca5162d9e5b
caps.latest.revision: "4"
author: BarbKess
ms.author: barbkess
manager: jhubbard
robots: noindex,nofollow
ms.workload: On Demand
ms.openlocfilehash: 967755e34b397f2dfac98277d34cb799655f5165
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="installation-and-configuration"></a>安装和配置
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]Wide World Importers OLTP 数据库安装和配置说明。

## <a name="prerequisites"></a>先决条件

- [SQL Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) （或更高版本） 或[Azure SQL 数据库](https://azure.microsoft.com/services/sql-database/)。 有关示例的完整版本，使用 SQL Server 评估/开发人员/企业版。
- [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md)。 为获得最佳结果使用 2016 年 6 月发行版或更高版本。

## <a name="download"></a>下载

最新版本中的示例：

[wide world 导入程序版本](http://go.microsoft.com/fwlink/?LinkID=800630)

将示例 WideWorldImporters 数据库备份/bacpac 下载对应到你的 SQL Server 或 Azure SQL 数据库版本。

从以下位置提供了源代码以重新创建示例数据库。 请注意由于在数据生成过程中没有随机因子，重新创建该示例将导致在数据的细微差异：

[wide world importers 计划](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-database-scripts)

## <a name="install"></a>Install


### <a name="sql-server"></a>SQL Server

若要将备份还原到的 SQL Server 实例，可以使用 Management Studio。

1. 打开 SQL Server Management Studio 并连接到目标 SQL Server 实例。
2. 右键单击**数据库**节点，然后选择**Restore Database**。
3. 选择**设备**并单击按钮**...**
4. 在对话框中**选择备份设备**，单击**添加**，导航到的服务器上，文件系统中的数据库备份，并选择的备份。 单击 **“确定”**。
5. 如果需要更改数据的目标位置，并在日志文件，**文件**窗格。 请注意，它将数据和日志文件的不同驱动器上的最佳做法。
6. 单击 **“确定”**。 这将启动数据库还原。 完成后，您将拥有数据库安装在 SQL Server 实例上的 WideWorldImporters。

### <a name="azure-sql-database"></a>Azure SQL Database

若要将 bacpac 导入新的 SQL 数据库，可以使用 Management Studio。

1. （可选）如果你还没有 SQL Server 在 Azure 中，导航到[Azure 门户](https://portal.azure.com/)并创建一个新的 SQL 数据库。 过程中创建数据库，你将创建的服务器。 请记下的服务器。
   - 请参阅[本教程](https://azure.microsoft.com/documentation/articles/sql-database-get-started/)在几分钟内创建数据库
2. 打开 SQL Server Management Studio 并连接到 Azure 中的服务器。
3. 右键单击**数据库**节点，然后选择**导入数据层应用程序**。
4. 在**导入设置**选择**从本地磁盘导入**和选择示例数据库的 bacpac 从您的文件系统。
5. 下**数据库设置**数据库名称更改为*WideWorldImporters*和选择要使用的目标版本和服务目标。
6. 单击**下一步**和**完成**可启动部署。 它将耗费几分钟才能完成 P1。 如果较低的定价层是所需，建议将导入新的 P1 数据库，然后将定价层更改为所需的级别。

## <a name="configuration"></a>配置

### <a name="full-text-indexing"></a>全文索引

示例数据库可使用的全文检索。 但是，默认情况下，与 SQL Server 未安装该功能-你需要在 SQL Server 安装程序 （默认情况下，Azure SQL 数据库中已启用） 期间选择它。 因此，安装后步骤是必需的。

1. 在 SQL Server Management Studio，连接到 WideWorldImporters 数据库并打开新查询窗口。
2. 运行以下的 T-SQL 命令，以启用在数据库中的全文索引使用：`EXECUTE Application.Configuration_ApplyFullTextIndexing`


### <a name="sql-server-audit"></a>SQL Server 审核

适用于： SQL Server

启用 SQL Server 中审核要求服务器配置。 若要启用 SQL Server 审核 WideWorldImporters 示例，请在数据库中运行以下语句：

    EXECUTE [Application].[Configuration_ApplyAuditing]

在 Azure SQL 数据库审核配置通过[Azure 门户](https://portal.azure.com/)。

### <a name="row-level-security"></a>行级安全性

适用范围： Azure SQL 数据库

默认情况下，在 WideWorldImporters bacpac 下载不启用行级别安全性。 若要在数据库中启用行级别安全性，请运行以下存储的过程：

    EXECUTE [Application].[Configuration_ApplyAuditing]

