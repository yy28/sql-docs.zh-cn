---
title: 将 Oracle HR 架构迁移到 Linux 上的 SQL Server |Microsoft Docs
description: 将示例 Oracle 架构转换为 Linux 上的 SQL Server
author: shamikg
ms.author: shamikg
manager: v-thobro
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: ''
ms.technology: ssma
ms.openlocfilehash: 312797b2b883f764fc65588e72cd67d7227e327a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62629787"
---
# <a name="migrate-an-oracle-schema-to-sql-server-2017-on-linux-with-the-sql-server-migration-assistant"></a>将 Oracle 架构迁移到 SQL Server 2017 Linux 上使用 SQL Server Migration Assistant

本教程使用 SQL Server Migration Assistant (SSMA) for Windows 上的 Oracle 转换 Oracle 示例**HR**架构[Linux 上的 SQL Server 2017](../../linux/sql-server-linux-overview.md)。

> [!div class="checklist"]
> * 下载并安装在 Windows 上的 SSMA
> * 创建 SSMA 项目来管理迁移
> * 连接到 Oracle
> * 运行迁移报告
> * 将示例 HR 架构转换
> * 将数据迁移

## <a name="prerequisites"></a>先决条件

- 实例的 Oracle 12c (12.2.0.1.0) 与**HR**架构安装
- Linux 上的 SQL Server 的工作实例

> [!NOTE]
> 到目标 SQL Server on Windows，可以使用相同的步骤，但必须选择中的 Windows**迁移到**项目设置。

## <a name="download-and-install-ssma-for-oracle"></a>下载并安装适用于 Oracle 的 SSMA

有几个版本的 SQL Server Migration Assistant，具体取决于您的源数据库。  下载最新版[SQL Server Migration Assistant for Oracle](https://aka.ms/ssmafororacle)和使用的下载页上找到的说明安装它。

> [!NOTE]
> 在此期间， **SSMA for Oracle 扩展包**不支持在 Linux 上，但不需要在本教程。

## <a name="create-and-set-up-project"></a>创建和设置项目

使用以下步骤创建一个新的 SSMA 项目：

1. 打开适用于 Oracle 的 SSMA 并选择**新的项目**从**文件**菜单。

1. 为项目指定名称。

1. 选择"SQL Server 2017 (Linux)-预览"中**迁移到**字段。

默认情况下，适用于 Oracle 的 SSMA 不使用 Oracle 示例架构。 若要启用 HR 架构，请使用以下步骤：

1. 在 SSMA 中选择**工具**菜单。

1. 选择**默认项目设置**，然后选择**加载系统对象**。

1. 请确保**HR**处于选中状态，然后选择**确定**。

## <a name="connect-to-oracle"></a>连接到 Oracle

接下来连接到 Oracle 的 SSMA。

1. 在工具栏上，单击**连接到 Oracle**。

1. 输入服务器名称、 端口、 Oracle SID、 用户名和密码。

   ![连接到 Oracle](./media/sql-server-linux-convert-from-oracle/ConnectToOracle.png)

1. 然后单击“连接” 。 在几分钟后，适用于 Oracle 的 SSMA 将连接到数据库并读取其元数据。

## <a name="create-a-report"></a>创建报表

使用以下步骤来生成迁移报告。

1. 在中**Oracle 元数据资源管理器**，展开服务器的节点。

1. 展开**架构**，右键单击**HR**，然后选择**创建报表**。

   ![Oracle 元数据资源管理器创建报表](./media/sql-server-linux-convert-from-oracle/CreateReport.png)

1. 新的浏览器窗口将打开与列出的所有警告和错误与转换相关联的报表。

   > [!NOTE]
   > 不需要为本教程中执行任何操作的列表。 如果用于 Oracle 数据库执行这些步骤，您应查看该报表，以便解决你的数据库的任何重要的转换问题。

   ![示例迁移报告](./media/sql-server-linux-convert-from-oracle/SSMAReport.png)

## <a name="connect-to-sql-server"></a>连接到 SQL Server

接下来，选择**连接到 SQL Server**并输入适当的连接信息。  如果使用的数据库名称，已不存在，适用于 Oracle 的 SSMA 将为你创建它。

![连接到 SQL Server](./media/sql-server-linux-convert-from-oracle/ConnectToSQLServer.png)

## <a name="convert-schema"></a>转换架构

右键单击**HR**中**Oracle 元数据资源管理器**，并选择将转换的架构。

![转换架构](./media/sql-server-linux-convert-from-oracle/ConvertSchema.png)

## <a name="synchronize-database"></a>同步数据库

接下来，将同步数据库。

1. 转换完成后，使用**SQL Server 元数据资源管理器**转到数据库中创建在上一步。

1. 右键单击数据库，选择**与数据库同步**，然后单击确定。

   ![将与数据库同步](./media/sql-server-linux-convert-from-oracle/SynchronizeWithDatabase.png)

## <a name="migrate-data"></a>将数据迁移

最后一步是将数据迁移。

1. 在**Oracle 元数据资源管理器**，右键单击**HR**，然后选择**迁移数据**。

1. 数据迁移步骤需要重新输入 Oracle 和 SQL Server 凭据。

1. 完成后，查看数据迁移报告，其中应类似于以下屏幕快照：

   ![数据迁移报表](./media/sql-server-linux-convert-from-oracle/DataMigrationReport.png)

## <a name="next-steps"></a>后续步骤

对于更复杂的 Orcale 架构，转换过程将涉及更多的时间、 测试和客户端应用程序可能发生的更改。 本教程的目的是介绍如何在整个迁移过程的一部分，用于 Oracle 使用 SSMA。

在本教程中，你将了解：
> [!div class="checklist"]
> * 在 Windows 上安装 SSMA
> * 创建新的 SSMA 项目
> * 评估并运行从 Oracle 迁移

接下来，了解使用 SSMA 的其他方法：

> [!div class="nextstepaction"]
>[SQL Server Migration Assistant 文档](../sql-server-migration-assistant.md)
