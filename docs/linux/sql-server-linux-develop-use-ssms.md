---
title: "管理使用 SSMS 的 Linux 上的 SQL Server |Microsoft 文档"
description: "本教程演示如何在 Windows 上使用 SQL Server Management Studio 连接到 SQL Server 在 Linux 上运行。"
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 30cc4564-f389-4707-9b25-8ba782cc5150
ms.workload: On Demand
ms.openlocfilehash: 98fdce174be9f7a3dc67d910a84f8558ede1b317
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2018
---
# <a name="use-sql-server-management-studio-ssms-on-windows-to-manage-sql-server-on-linux"></a>使用 Windows 上的 SQL Server Management Studio (SSMS) 管理 Linux 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本主题演示如何使用[SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)连接到 Linux 上的 SQL Server 2017。 SSMS 是一个 Windows 应用程序，因此请在 Windows 计算机可连接到 Linux 上的远程 SQL Server 实例时使用 SSMS。

成功连接后，请运行简单的 Transact - SQL (T-SQL) 查询，验证与数据库的通信。

## <a name="install-the-newest-version-of-sql-server-management-studio"></a>安装最新版本的 SQL Server Management Studio

使用 SQL Server 时，应始终使用最新版本的 SQL Server Management Studio (SSMS)。 最新版本的 SSMS 不断更新和优化并且当前适用于 SQL Server 2017 on Linux。 若要下载并安装最新版本，请参阅[下载 SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)。 为保持使用最新版本，有可供下载的新版本时，最新版本的 SSMS 会发出提示。 

## <a name="connect-to-sql-server-on-linux"></a>连接到 Linux 上的 SQL Server

以下步骤演示了如何使用 SSMS 连接到 Linux 版 SQL Server 2017。

1. 启动 SSMS，通过键入**Microsoft SQL Server Management Studio**在窗口中搜索框中，并依次桌面应用程序。

    ![SQL Server Management Studio](./media/sql-server-linux-develop-use-ssms/ssms.png)

2. 在**连接到服务器**窗口中，输入以下信息 (如果已在运行 SSMS，请单击**连接 > 数据库引擎**以打开**连接到服务器**窗口):

   | 设置 | Description |
   |-----|-----|
   | **服务器类型** | 默认为数据库引擎；请勿更改此值。 |
   | **服务器名称** | 输入目标 Linux SQL Server 计算机的名称或它的 IP 地址。 |
   | **身份验证** | 在 Linux 上的 SQL Server 2017，对于使用**SQL Server 身份验证**。 |
   | **登录** | 输入数据库服务器上具有权限的用户的名称 (例如，默认值**SA**安装过程中创建的帐户)。 |
   | **密码** | 为指定的用户输入密码 (为**SA**帐户，则此安装过程中创建)。 |

    ![SQL Server Management Studio： 连接到 SQL 数据库服务器](./media/sql-server-linux-develop-use-ssms/connect.png)

3. 单击 **“连接”**。

    > [!TIP]
    > 如果连接失败，请首先尝试根据错误消息诊断问题。 然后查看[连接故障排除建议](sql-server-linux-troubleshooting-guide.md#connection)。
 
5. 已成功连接到你 SQL Sever 后**对象资源管理器**，你现在可以访问你的数据库执行管理任务或查询数据。
 
     ![对象资源管理器](./media/sql-server-linux-develop-use-ssms/object-explorer.png)
     
## <a name="run-sample-queries"></a>运行示例查询

连接到服务器后，可以连接到数据库并运行示例查询。 如果你不熟悉如何编写查询，请参阅[编写 TRANSACT-SQL 语句](../t-sql/tutorial-writing-transact-sql-statements.md)。

1. 标识要使用的数据库，再次运行查询。 这可能是您在创建新数据库[TRANSACT-SQL 教程](../t-sql/tutorial-writing-transact-sql-statements.md)。 也可能是**AdventureWorks**示例数据库，您[下载并还原](sql-server-linux-migrate-restore-database.md)。
2. 在**对象资源管理器**，导航到服务器上的目标数据库。
2. 右键单击数据库，然后选择**新查询**:

    ![新查询。 连接到 SQL 数据库服务器： SQL Server Management Studio](./media/sql-server-linux-develop-use-ssms/new-query.png)

3. 在查询窗口中，编写 Transact - SQL 查询，从其中一个表中选择数据。 下面的示例选择从数据**Production.Product**表**AdventureWorks**数据库。

        SELECT TOP 10 Name, ProductNumber
        FROM Production.Product
        ORDER BY Name ASC

4. 单击**执行**按钮：

    ![成功。 连接到 SQL 数据库服务器： SQL Server Management Studio](./media/sql-server-linux-develop-use-ssms/execute-query.png)

## <a name="next-steps"></a>后续步骤

除查询外，还可使用 T-SQL 语句创建和管理数据库。

如果你不熟悉 T-SQL 的请参阅[教程： 编写 TRANSACT-SQL 语句](../t-sql/tutorial-writing-transact-sql-statements.md)和[TRANSACT-SQL 参考 （数据库引擎）](https://msdn.microsoft.com/library/bb510741.aspx)。

有关如何使用 SSMS 的详细信息，请参阅[使用 SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx)。
