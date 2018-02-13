---
title: "开发和部署 SQL Server databases 适用于 Linux |Microsoft 文档"
description: 
author: erickangMSFT
ms.author: erickang
manager: jroth
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.technology: database-engine
ms.assetid: 1e924704-e07c-4a8b-b243-8c1dd8cff0d3
ms.custom: sql-linux
ms.workload: On Demand
ms.openlocfilehash: 0ff7526517be55100400da6ac84b6f7c927fb50e
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/13/2018
---
# <a name="use-visual-studio-to-create-databases-for-sql-server-on-linux"></a>使用 Visual Studio 为 Linux 上的 SQL Server 创建数据库

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server Data Tools (SSDT) 可将 Visual Studio 转变为一种强大的开发环境和数据库生命周期管理 (DLM) 环境，转变后的环境适用于 Linux 上的 SQL Server。 你可以开发、 生成、 测试和发布你的数据库从源代码管理的项目，就像你开发应用程序代码。

## <a name="install-visual-studio-and-sql-server-data-tools"></a>安装 Visual Studio 和 SQL Server Data Tool

1. 如果你尚未安装 Visual Studio 在 Windows 计算机上[下载和安装 Visual Studio]。 如果你没有 Visual Studio 许可证，Visual Studio Community edition 是学生版的免费的完整功能 IDE 的开源和各个开发人员。

2. 在 Visual Studio 安装过程中选择**自定义**为**选择安装类型**选项。 单击 **“下一步”**

3. 选择**Microsoft SQL Server Data Tools**， **Git for Windows**，和**的 Visual Studio 的 GitHub 扩展**从功能选择列表中。

    <img src="./media/sql-server-linux-develop-use-ssdt/ssdt-setup.png" alt="ssdt setup" style="width: 400px;"/>

4. 继续完成 Visual Studio 安装。 这可能需要几分钟。

## <a name="upgrade-sql-server-data-tools-to-ssdt-170-rc-release"></a>将 SQL Server Data Tools 升级到 SSDT 17.0 RC 版本

在 Linux 上的 SQL Server 2017 受 SSDT 版本 17.0 RC 或更高版本。

* [下载并安装 SSDT 17.0 RC2](https://go.microsoft.com/fwlink/?linkid=837939)。

## <a name="create-a-new-database-project-in-source-control"></a>在源控件中创建新数据库项目

1. 启动 Visual Studio。

2. 选择**团队资源管理器**上**视图**菜单。 

3. 单击**新建**中**本地 Git 存储库**节**连接**页。

    <img src="./media/sql-server-linux-develop-use-ssdt/git-repository.png" alt="local repository" style="width: 300px;"/>

3. 单击 **“创建”**。 创建本地 Git 存储库后，双击**SSDTRepo**。

4. 单击**新建**中**解决方案**部分。 选择**SQL Server**下**其他语言**中的节点**新项目**对话框。

    <img src="./media/sql-server-linux-develop-use-ssdt/new-project.png" alt="local repository" style="width: 480px;"/>

5. 键入**TutorialDB**的名称，然后单击**确定**创建新的数据库项目。

## <a name="create-a-new-table-in-the-database-project"></a>在数据库项目中创建新表

1. 选择**解决方案资源管理器**上**视图**菜单。

2. 通过右键单击打开数据库项目菜单**TutorialDB**在解决方案资源管理器。

3. 选择**表**下**添加**。

    <img src="./media/sql-server-linux-develop-use-ssdt/create-table.png" alt="create table" style="width: 480px;"/>

4. 使用表设计器中，添加两个列，名称`nvarchar(50)`和位置`nvarchar(50)`，如图所示。 SSDT 生成`CREATE TABLE`脚本当设计器中添加列。

    <img src="./media/sql-server-linux-develop-use-ssdt/add-columns.png" alt="add columns" style="width: 480px;"/>

5. 保存**Table1.sql**文件。

## <a name="build-and-validate-the-database"></a>生成和验证数据库

1. 打开数据库项目菜单上**TutorialDB**和选择**生成**。 SSDT 将在项目中编译 .sql 源代码文件，并生成数据层应用程序包 (dacpac) 文件。 这适用于将数据库发布到 Linux 上的 SQL Server 2017 实例。 

    <img src="./media/sql-server-linux-develop-use-ssdt/build.png" alt="add columns" style="width: 400px;"/>

2. 请检查中的生成成功消息**输出**Visual Studio 中的窗口。 

## <a name="publish-the-database-to-sql-server-2017-instance-on-linux"></a>将数据库发布到 Linux 上的 SQL Server 2017 实例

1. 打开数据库项目菜单上**TutorialDB**和选择**发布**。

2. 单击**编辑**以选择你在 Linux 上的 SQL Server 实例。

    <img src="./media/sql-server-linux-develop-use-ssdt/publish-dialog.png" alt="publish dialog" style="width: 480px;"/>

3. 在连接对话框中，键入 IP 地址或 Linux 上的 SQL Server 实例的主机名、用户名和密码。

    <img src="./media/sql-server-linux-develop-use-ssdt/connection-dialog.png" alt="connection dialog" style="width: 400px;"/>

4. 单击**发布**发布对话框上的按钮。

5. 请检查中的发布状态**数据工具操作**窗口。

6. 单击**视图 Reulst**或**查看脚本**若要查看的数据库的详细信息发布在 Linux 上 SQL Server 上的结果。

    <img src="./media/sql-server-linux-develop-use-ssdt/publish-result.png" alt="publish result" style="width: 480px;"/>

已成功在 Linux 上的 SQL Server 实例上创建新数据库并了解开发具有受源代码管理数据库项目的数据库的基础知识。

## <a name="next-steps"></a>后续步骤

如果你不熟悉 T-SQL 的请参阅[教程： 编写 TRANSACT-SQL 语句]和[TRANSACT-SQL 参考 （数据库引擎）]。

有关开发具有 SQL Data Tools 的数据库的详细信息，请参阅[SSDT MSDN 文档]

[下载和安装 Visual Studio]:https://www.visualstudio.com/downloads/
[Download and Install SSDT 17.0 RC2]:https://aka.ms/ssdt-download
[SSDT MSDN 文档]: https://msdn.microsoft.com/en-us/library/hh272686(v=vs.103).aspx
[教程： 编写 TRANSACT-SQL 语句]:https://msdn.microsoft.com/library/ms365303.aspx
[TRANSACT-SQL 参考 （数据库引擎）]:https://msdn.microsoft.com/library/bb510741.aspx
