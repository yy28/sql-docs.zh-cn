---
title: 将 DB2 数据迁移到 SQL Server (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 86cbd39f-6dac-409a-9ce1-7dd54403f84b
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: c64b1ea3ecc283cdea92a5722c7a1dad120ecb50
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52395180"
---
# <a name="migrating-db2-data-into-sql-server-db2tosql"></a>将 DB2 数据迁移到 SQL Server (DB2ToSQL)
已成功同步与已转换的对象后[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，可以将数据从 DB2 到迁移[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
> [!IMPORTANT]  
> 如果正在使用的引擎是服务器端数据迁移引擎，然后，你可以迁移数据，则必须安装 SSMA DB2 的扩展包，和运行 SSMA 的计算机上的 DB2 提供程序。 此外必须运行 SQL Server 代理服务。 有关如何安装扩展包的详细信息，请参阅[SQL Server 上安装 SSMA 组件](https://msdn.microsoft.com/cf2b724b-4ca7-470a-8dd7-fa95b1e060a4)  
  
## <a name="setting-migration-options"></a>设置迁移选项  
在迁移之前，数据到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，查看中的项目迁移选项**项目设置**对话框。  
  
-   通过使用此对话框可以设置选项，如迁移批大小、 表锁定、 约束检查，空值处理和标识值处理。 有关项目迁移设置的详细信息，请参阅[项目设置 （迁移）](https://msdn.microsoft.com/48aaa8e6-a9cb-487d-9ba5-fc3f1c4786ae)。  
  
-   **迁移引擎**中**项目设置**对话框，允许用户执行迁移过程使用两种类型的数据迁移引擎：  
  
    1.  客户端数据迁移引擎  
  
    2.  服务器端数据迁移引擎  
  
**客户端将数据迁移：**  
  
-   若要启动数据迁移客户端上，选择**客户端数据迁移引擎**选项**项目设置**对话框。  
  
-   在中**项目设置**，则**客户端数据迁移引擎**设置选项。  
  
    > [!NOTE]  
    > **客户端的数据迁移引擎**驻留在 SSMA 应用程序内，并且是，因此，不依赖于扩展包的可用性。  
  
**服务器端数据迁移：**  
  
-   在服务器端数据迁移期间，引擎驻留在目标数据库上。 它通过扩展包安装。 有关如何安装扩展包的详细信息，请参阅[SQL Server 上安装 SSMA 组件](https://msdn.microsoft.com/cf2b724b-4ca7-470a-8dd7-fa95b1e060a4)  
  
-   若要启动的服务器端上的迁移，选择**服务器端数据迁移引擎**选项**项目设置**对话框。  
  
## <a name="migrating-data-to-sql-server"></a>将数据迁移到 SQL Server  
迁移数据是将数据行移到的 DB2 表中大容量加载操作[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]事务中的表。 加载到的行数[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在每个事务在项目设置中配置。  
  
若要查看迁移的消息，请确保输出窗格可见。 否则为从**视图**菜单中，选择**输出**。  
  
**若要将数据迁移**  
  
1.  检查下列各项：  
  
    -   正在运行的 SSMA 在计算机上安装的 DB2 提供程序。  
  
    -   你已将同步转换后的对象与[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库。  
  
2.  在 DB2 元数据资源管理器，选择包含你想要迁移的数据的对象：  
  
    -   若要迁移的所有架构的数据，选择复选框旁边**架构**。  
  
    -   若要将数据迁移或忽略各个表，首先展开架构，展开**表**，然后选中或清除表旁边的复选框。  
  
3.  若要将数据迁移，两种情况下出现：  
  
    **客户端将数据迁移：**  
  
    -   用于执行**客户端数据迁移**，选择**客户端数据迁移引擎**选项**项目设置**对话框。  
  
    **服务器端数据迁移：**  
  
    -   之前在服务器端执行数据迁移，请确保：  
  
        1.  实例上安装 SSMA for DB2 的扩展包， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
        2.  SQL Server 实例上运行的 SQL Server 代理服务。  
  
    -   用于执行**服务器端数据迁移**，选择**服务器端数据迁移引擎**选项**项目设置**对话框。  
  
4.  右键单击**架构**在 DB2 元数据资源管理器，然后单击**迁移数据**。 此外可以将迁移为单个对象或类别的对象的数据：右键单击该对象或其父文件夹;选择**迁移数据**选项。  
  
    > [!NOTE]  
    > SSMA for DB2 的扩展包，如果未安装的实例上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，并且如果**服务器端数据迁移引擎**选中，那么在将数据迁移到目标数据库，时遇到以下错误：SQL Server 上找不到 SSMA 数据迁移组件，无法在服务器端数据迁移。 请检查是否正确安装的扩展包。 单击**取消**终止数据迁移。  
  
5.  在中**连接到 DB2**对话框中，输入连接凭据，然后单击**Connect**。 连接到 DB2 的详细信息，请参阅[连接到 DB2 数据库&#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md)  
  
    用于连接到目标数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，输入中的连接凭据**连接到 SQL Server**对话框中，然后单击**Connect**。 有关详细信息连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请参阅[连接到 SQL Server](https://msdn.microsoft.com/b59803cb-3cc6-41cc-8553-faf90851410e)  
  
    消息将出现在**输出**窗格。 在迁移完成后，**数据迁移报表**出现。 如果未迁移的任何数据，单击包含错误的行，然后单击**详细信息**。 与报表一起完成后，单击**关闭**。 数据迁移报表的详细信息，请参阅[数据迁移报表 （SSMA 常见）](https://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> 如果 SQL Express 版本用作目标数据库，则允许仅限客户端数据迁移，并且不支持服务器端数据迁移。  
  
## <a name="see-also"></a>请参阅  
[将 DB2 数据迁移到 SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
  
