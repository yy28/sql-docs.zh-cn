---
title: 安装&配置 DW 广域世界进口商示例数据库
description: 按照这些说明使用 SQL Server 管理工作室下载、安装和配置 WideWorld 导入者DW 示例数据库。
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 08/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: 2f640415ecdc2ae4a48220aeec2a2c78ed79807c
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488537"
---
# <a name="wideworldimportersdw-installation-and-configuration"></a>广域国际进口商DW安装和配置
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
宽世界进口商DW数据库的安装和配置说明。

- [SQL 服务器 2016（](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)或更高）或[Azure SQL 数据库](https://azure.microsoft.com/services/sql-database/)。 要使用示例的完整版本，请使用 SQL 服务器评估/开发人员/企业版。
- [SQL 服务器管理工作室](../ssms/download-sql-server-management-studio-ssms.md)。 为获得最佳效果，请使用 2016 年 6 月版本或更高版本。

## <a name="download"></a>下载

示例的最新版本：

[全球进口商发布](https://go.microsoft.com/fwlink/?LinkID=800630)

下载与 SQL Server 或 Azure SQL 数据库版本对应的示例 WideWorld 导入者DW 数据库备份/bacpac。

要重新创建示例数据库的源代码可从以下位置获得。 请注意，数据填充基于 OLTP 数据库（WideWorld导入器）的 ETL：

[全球进口商-来源](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts)

## <a name="install"></a>安装


### <a name="sql-server"></a>SQL Server

要将备份还原到 SQL Server 实例，可以使用管理工作室。

1. 打开 SQL 服务器管理工作室并连接到目标 SQL Server 实例。
2. 右键单击**数据库**节点，然后选择 **"还原数据库**"。
3. 选择**设备**并单击按钮 **...**
4. 在对话框中选择**备份设备**，单击"**添加**"，导航到服务器文件系统中的数据库备份，然后选择备份。 单击“确定”。 
5. 如果需要，请更改"**文件"** 窗格中数据和日志文件的目标位置。 请注意，最佳做法是将数据和日志文件放在不同的驱动器上。
6. 单击“确定”。  这将启动数据库还原。 完成后，您将在 SQL Server 实例上安装数据库 WideWorld 导入器。

### <a name="azure-sql-database"></a>Azure SQL Database

要将百家乐导入新的 SQL 数据库，可以使用管理工作室。

1. （可选）如果 Azure 中尚未有 SQL 服务器，请导航到[Azure 门户](https://portal.azure.com/)并创建新的 SQL 数据库。 在创建数据库的过程中，您将创建一个服务器。 记下服务器。
   - 请参阅[本教程](https://azure.microsoft.com/documentation/articles/sql-database-get-started/)，在几分钟内创建数据库
2. 打开 SQL 服务器管理工作室并连接到 Azure 中的服务器。
3. 右键单击**数据库**节点，然后选择**导入数据层应用程序**。
4. 在"**导入设置"** 中选择 **"从本地磁盘导入**"，然后从文件系统中选择示例数据库的百科。
5. 在 **"数据库设置"** 下，将数据库名称更改为*WideWorld 导入者DW，* 并选择要使用的目标版本和服务目标。
6. 单击"**下一步**"并**完成**以启动部署。 完成此部署可能需要几分钟时间。 指定低于 S2 的服务目标时，可能需要更长时间。

## <a name="configuration"></a>配置

[适用于 SQL Server 2016（及以后）开发人员/评估/企业版]

示例数据库可以使用 PolyBase 查询 Hadoop 或 Azure Blob 存储中的文件。 但是，默认情况下，SQL Server 不会安装该功能 - 您需要在 SQL Server 设置期间选择它。 因此，需要安装后步骤。

1. 在 SQL 服务器管理工作室中，连接到宽世界导入者DW数据库并打开一个新的查询窗口。
2. 运行以下 T-SQL 命令，以便在数据库中使用 PolyBase：

   执行 [应用程序]。[Configuration_ApplyPolyBase]
