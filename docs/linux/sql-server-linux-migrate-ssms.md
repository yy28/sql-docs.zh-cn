---
title: 导出和导入 Linux 上的数据库 |Microsoft 文档
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.technology: linux
ms.assetid: 2210cfc3-c23a-4025-a551-625890d6845f
ms.custom: sql-linux
ms.openlocfilehash: 7a7c1c73ca70e0d42104e74c868d6acd32cc01b1
ms.sourcegitcommit: b5ab9f3a55800b0ccd7e16997f4cd6184b4995f9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2018
ms.locfileid: "34454880"
---
# <a name="export-and-import-a-database-on-linux-with-ssms-or-sqlpackageexe-on-windows"></a>导出和导入与 SSMS 或 Windows 上的 SqlPackage.exe Linux 上的数据库

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

这篇文章演示如何使用[SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)和[SqlPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx)导出和导入在 Linux 上的 SQL Server 2017 上的数据库。 SSMS 和 SqlPackage.exe 是 Windows 应用程序，因此使用此方法，当你有一台 Windows 计算机可以连接到 Linux 上的远程 SQL Server 实例。

应始终安装并使用最新版本的 SQL Server Management Studio (SSMS) 中所述[以连接到 Linux 上的 SQL Server 的 Windows 上使用 SSMS](sql-server-linux-manage-ssms.md)

> [!NOTE]
> 如果你要从一个 SQL Server 实例到另一个迁移数据库，建议是使用[备份和还原](sql-server-linux-migrate-restore-database.md)。

## <a name="export-a-database-with-ssms"></a>使用 SSMS 导出数据库

1. 启动 SSMS，通过键入**Microsoft SQL Server Management Studio**在窗口中搜索框中，并依次桌面应用程序。

    ![SQL Server Management Studio](./media/sql-server-linux-manage-ssms/ssms.png) 

2. 在对象资源管理器中连接到源数据库。 源数据库可以位于在本地或云中、在 Linux、Windows 或 Docker 上以及在 Azure SQL 数据库或 Azure SQL 数据仓库中运行的 Microsoft SQL Server 中。

3. 右键单击对象资源管理器中的源数据库，指向**任务**，然后单击**导出数据层应用程序...**

4. 在导出向导中，单击**下一步**，然后在**设置**选项卡上，配置导出，以将 BACPAC 文件保存到本地磁盘位置或 Azure blob。

5. 默认情况下，将导出数据库中的所有对象。 单击**高级选项卡**，然后选择你想要导出的数据库对象。

6. 单击 **“下一步”** ，然后单击 **“完成”**。

*.BACPAC 文件已成功在所选位置创建，并且可以开始将该文件导入目标数据库。

## <a name="import-a-database-with-ssms"></a>使用 SSMS 导入数据库

1. 启动 SSMS，通过键入**Microsoft SQL Server Management Studio**在窗口中搜索框中，并依次桌面应用程序。

    ![SQL Server Management Studio](./media/sql-server-linux-manage-ssms/ssms.png) 

2. 在对象资源管理器中连接到目标服务器。 目标服务器可在本地运行的 Microsoft SQL Server 或在云中，在 Linux、 Windows 或 Docker 和 Azure SQL 数据库或 Azure SQL 数据仓库上。

3. 右键单击**数据库**文件夹中的对象资源管理器和单击**导入数据层应用程序...**

4. 若要在目标服务器中创建数据库，需指定本地磁盘中的 BACPAC 文件，或选择已将 BACPAC 文件上传到的 Azure 存储帐户和容器。

5. 为数据库提供新的数据库名称。 如果要在 Azure SQL 数据库上导入数据库，请设置 Microsoft Azure SQL 数据库的版本（服务层）、最大数据库大小和服务目标（性能级别）。

6. 单击**下一步**，然后单击**完成**BACPAC 文件导入到你在目标服务器中的新数据库。

*.BACPAC 文件已成功导入，以在指定的目标服务器中创建新数据库。

## <a id="sqlpackage"></a> SqlPackage 命令行选项

还有可能要使用 SQL Server Data Tools (SSDT) 命令行工具， [SqlPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx)，若要将导出和导入 BACPAC 文件。

以下示例命令导出 BACPAC 文件：

```bash
SqlPackage.exe /a:Export /ssn:tcp:<your_server> /sdn:<your_database> /su:<username> /sp:<password> /tf:<path_to_bacpac>
```

使用以下命令从 .BACPAC 文件导入数据库架构和用户数据：

```bash
SqlPackage.exe /a:Import /tsn:tcp:<your_server> /tdn:<your_database> /tu:<username> /tp:<password> /sf:<path_to_bacpac>

```

## <a name="see-also"></a>另请参阅
有关如何使用 SSMS 的详细信息，请参阅[使用 SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx)。 SqlPackage.exe 的详细信息，请参阅[SqlPackage 参考文档](https://msdn.microsoft.com/library/hh550080.aspx)。
