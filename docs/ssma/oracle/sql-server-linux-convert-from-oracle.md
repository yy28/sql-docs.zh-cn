---
title: 将 Oracle HR 架构迁移到 SQL Server on Linux |Microsoft 文档
description: 将示例 Oracle 架构转换为在 Linux 上的 SQL Server
author: edmacauley
ms.author: edmacauley
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql
ms.suite: sql
ms.custom: ''
ms.technology: database-engine
ms.openlocfilehash: 6c92ab25e4401c4a4e6d1591c03d5702cca77944
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2018
ms.locfileid: "34778113"
---
# <a name="migrate-an-oracle-schema-to-sql-server-2017-on-linux-with-the-sql-server-migration-assistant"></a>将 Oracle 架构迁移到使用 SQL Server Migration Assistant Linux 上的 SQL Server 2017

本教程使用的 Windows 上的 Oracle SQL Server 迁移助手 (SSMA) 来转换 Oracle 示例**HR**架构[在 Linux 上的 SQL Server 2017](../../linux/sql-server-linux-overview.md)。

> [!div class="checklist"]
> * 下载并安装在 Windows 上的 SSMA
> * 创建一个 SSMA 项目以管理迁移
> * 连接到 Oracle
> * 运行迁移报告
> * 将示例 HR 架构转换
> * 迁移数据

## <a name="prerequisites"></a>必要條件

- 实例的 Oracle 12c (12.2.0.1.0) **HR**架构安装
- 在 Linux 上的 SQL Server 的工作实例

> [!NOTE]
> 到目标 SQL Server 在 Windows 上，可以使用相同的步骤，但你必须选择在 Windows**迁移到**项目设置。

## <a name="download-and-install-ssma-for-oracle"></a>下载并安装适用于 Oracle 的 SSMA

有几个版本的 SQL Server Migration Assistant 可用，具体取决于你的源数据库。  下载最新版本的[SQL Server Migration Assistant for Oracle](http://aka.ms/ssmafororacle)和使用的下载页上找到的说明安装它。

> [!NOTE]
> 在此期间， **Oracle 扩展包的 SSMA**不支持在 Linux 上，但不需要对于本教程。

## <a name="create-and-set-up-project"></a>创建和设置项目

使用以下步骤创建新的 SSMA 项目：

1. 打开适用于 Oracle 的 SSMA 并选择**新项目**从**文件**菜单。

1. 为项目的名称。

1. 在中选择"SQL Server 2017 (Linux)-预览"**迁移到**字段。

默认情况下，适用于 Oracle 的 SSMA 不使用 Oracle 示例架构。 若要启用 HR 架构，请使用以下步骤：

1. SSMA，在选择**工具**菜单。

1. 选择**默认项目设置**，然后选择**加载系统对象**。

1. 请确保**HR**已选中，然后选择**确定**。

## <a name="connect-to-oracle"></a>连接到 Oracle

接下来连接到 Oracle 的 SSMA。

1. 在工具栏上，单击**连接到 Oracle**。

1. 输入服务器名称、 端口、 Oracle SID、 用户名和密码。

   ![连接到 Oracle](./media/sql-server-linux-convert-from-oracle/ConnectToOracle.png)

1. 然后单击“连接” 。 花费几分钟，适用于 Oracle 的 SSMA 连接到你的数据库，并读取其元数据。

## <a name="create-a-report"></a>创建报表

使用以下步骤来生成迁移报告。

1. 在**Oracle 元数据资源管理器**，展开你的服务器的节点。

1. 展开**架构**，右键单击**HR**，然后选择**创建报表**。

   ![Oracle 元数据资源管理器创建报表](./media/sql-server-linux-convert-from-oracle/CreateReport.png)

1. 与列出的警告和错误与转换相关联的所有报表会打开一个新的浏览器窗口。

   > [!NOTE]
   > 你不必执行任何操作与该列表出于本教程。 如果用于 Oracle 数据库中执行这些步骤时，应查看该报表来解决你的数据库的任何重要转换问题。

   ![示例迁移报告](./media/sql-server-linux-convert-from-oracle/SSMAReport.png)

## <a name="connect-to-sql-server"></a>连接到 SQL Server

接下来选择**连接到 SQL Server**并输入适当的连接信息。  如果你使用的数据库名称，已不存在，适用于 Oracle 的 SSMA 为你创建它。

![连接到 SQL Server](./media/sql-server-linux-convert-from-oracle/ConnectToSQLServer.png)

## <a name="convert-schema"></a>转换架构

右键单击**HR**中**Oracle 元数据资源管理器**，然后选择将转换的架构。

![转换架构](./media/sql-server-linux-convert-from-oracle/ConvertSchema.png)

## <a name="synchronize-database"></a>同步数据库

接下来，将你的数据库同步。

1. 转换完成后，使用**SQL 服务器元数据资源管理器**转到数据库中创建上一步。

1. 右键单击数据库，选择**与数据库的同步**，然后单击确定。

   ![与数据库进行同步](./media/sql-server-linux-convert-from-oracle/SynchronizeWithDatabase.png)

## <a name="migrate-data"></a>迁移数据

最后一步是将数据迁移。

1. 在**Oracle 元数据资源管理器**，右键单击**HR**，然后选择**迁移数据**。

1. 数据迁移步骤需要你重新输入 Oracle 和 SQL Server 凭据。

1. 完成后，查看数据迁移报告，其中应类似于以下屏幕快照：

   ![数据迁移报告](./media/sql-server-linux-convert-from-oracle/DataMigrationReport.png)

## <a name="next-steps"></a>后续步骤

对于更复杂的 Orcale 架构，则转换过程将涉及更多的时间、 测试和客户端应用程序可能发生的更改。 本教程的目的是演示如何作为整体的迁移过程的一部分，对于 Oracle 使用 SSMA。

在本教程中，您学习了如何：
> [!div class="checklist"]
> * 在 Windows 上安装 SSMA
> * 创建新的 SSMA 项目
> * 评估并从 Oracle 运行迁移

接下来，了解使用 SSMA 的其他方式：

> [!div class="nextstepaction"]
>[SQL Server Migration Assistant 文档](../sql-server-migration-assistant.md)
