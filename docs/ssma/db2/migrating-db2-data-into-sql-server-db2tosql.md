---
title: "将 DB2 数据迁移到 SQL Server (DB2ToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 86cbd39f-6dac-409a-9ce1-7dd54403f84b
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 392deeac6aeb1791322723367def8f2e3e6464e8
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="migrating-db2-data-into-sql-server-db2tosql"></a>将 DB2 数据迁移到 SQL Server (DB2ToSQL)
已成功同步与已转换的对象后[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，可以将数据从 DB2 到迁移[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
> [!IMPORTANT]  
> 如果正在使用的引擎是服务器端数据迁移引擎，然后，你才能迁移数据，则必须安装 SSMA DB2 扩展包和运行 SSMA 的计算机上的 DB2 提供程序。 也必须运行 SQL Server 代理服务。 有关如何安装扩展包的详细信息，请参阅[SQL 服务器上安装 SSMA 组件](http://msdn.microsoft.com/en-us/cf2b724b-4ca7-470a-8dd7-fa95b1e060a4)  
  
## <a name="setting-migration-options"></a>设置迁移选项  
在迁移之前，数据到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，查看中的项目迁移选项**项目设置**对话框。  
  
-   通过使用此对话框可以设置迁移批大小、 表锁定、 约束检查、 null 值处理和标识值处理等选项。 有关项目迁移设置的详细信息，请参阅[项目设置 （迁移）](http://msdn.microsoft.com/en-us/48aaa8e6-a9cb-487d-9ba5-fc3f1c4786ae)。  
  
-   **迁移引擎**中**项目设置**对话框中，允许用户执行迁移过程使用两种类型的数据迁移引擎：  
  
    1.  客户端数据迁移引擎  
  
    2.  服务器端数据迁移引擎  
  
**客户端将数据迁移：**  
  
-   若要启动客户端上的数据迁移，选择**客户端数据迁移引擎**选项**项目设置**对话框。  
  
-   在**项目设置**、**客户端数据迁移引擎**设置选项。  
  
    > [!NOTE]  
    > **客户端数据迁移引擎**驻留在 SSMA 应用程序内和，因此是不依赖于扩展包的可用性。  
  
**服务器端数据迁移：**  
  
-   服务器端数据在迁移期间，引擎驻留在目标数据库。 通过扩展包安装它。 有关如何安装扩展包的详细信息，请参阅[SQL 服务器上安装 SSMA 组件](http://msdn.microsoft.com/en-us/cf2b724b-4ca7-470a-8dd7-fa95b1e060a4)  
  
-   若要启动的服务器端上的迁移，选择**服务器端数据迁移引擎**选项**项目设置**对话框。  
  
## <a name="migrating-data-to-sql-server"></a>将数据迁移到 SQL Server  
迁移数据是将数据行移到的 DB2 表中大容量加载操作[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]在事务中的表。 载入的行数[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]在每个事务在项目设置中配置。  
  
若要查看迁移消息，请确保输出窗格是可见。 否则为从**视图**菜单上，选择**输出**。  
  
**若要将数据迁移**  
  
1.  检查下列各项：  
  
    -   DB2 提供程序安装在运行 SSMA 的计算机上。  
  
    -   你已同步已转换的对象与[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库。  
  
2.  在 DB2 元数据资源管理器，选择包含你想要迁移的数据的对象：  
  
    -   若要迁移的所有架构的数据，请旁边选中的复选框**架构**。  
  
    -   若要将数据迁移或省略各个表，首先展开架构，展开**表**，然后选择或清除的表旁边的复选框。  
  
3.  若要将数据迁移，两种情况下出现：  
  
    **客户端将数据迁移：**  
  
    -   用于执行**客户机端数据迁移**，选择**客户端数据迁移引擎**选项**项目设置**对话框。  
  
    **服务器端数据迁移：**  
  
    -   在服务器端执行数据迁移，请确保：  
  
        1.  SSMA for DB2 扩展包的实例上安装[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
        2.  SQL Server 代理服务正在运行的 SQL Server 实例上。  
  
    -   用于执行**服务器端数据迁移**，选择**服务器端数据迁移引擎**选项**项目设置**对话框。  
  
4.  右键单击**架构**在 DB2 元数据资源管理器，然后单击**迁移数据**。 此外可以将迁移为单个对象或对象的类别的数据： 右键单击该对象或其父文件夹;选择**迁移数据**选项。  
  
    > [!NOTE]  
    > 如果实例上未安装 DB2 扩展包的 SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，并且如果**服务器端数据迁移引擎**选中，那么在将数据迁移到目标数据库，遇到以下错误: SSMA 数据迁移组件上未找到 SQL Server，将无法进行服务器端数据迁移。 请检查是否正确安装了扩展包。 单击**取消**终止数据迁移。  
  
5.  在**连接到 DB2**对话框中，输入连接凭据，，然后单击**连接**。 连接到 DB2 的详细信息，请参阅[连接到 DB2 数据库 &#40; DB2ToSQL &#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md)  
  
    用于连接到目标数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，输入中的连接凭据**连接到 SQL Server**对话框中，单击**连接**。 有关详细信息连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，请参阅[连接到 SQL Server](http://msdn.microsoft.com/en-us/b59803cb-3cc6-41cc-8553-faf90851410e)  
  
    消息将出现在**输出**窗格。 在迁移完成后，**数据迁移报告**显示。 如果任何数据未迁移，单击包含错误的行，然后单击**详细信息**。 在完成与报表，请单击**关闭**。 有关数据迁移报表的详细信息，请参阅[（SSMA 常见） 的数据迁移报告](http://msdn.microsoft.com/en-us/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> 当为目标数据库使用 SQL Express edition 时，允许仅限客户端数据迁移，并且不支持服务器端数据迁移。  
  
## <a name="see-also"></a>另请参阅  
[将 DB2 数据迁移到 SQL Server &#40; DB2ToSQL &#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
  

