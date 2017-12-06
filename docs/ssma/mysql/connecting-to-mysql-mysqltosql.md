---
title: "连接到 MySQL (MySQLToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-mysql
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Connecting to MySQL, MySQL permission
- Connecting to MySQL,reconnecting
ms.assetid: 084c7020-f729-4f91-90e0-143f85fa68d1
caps.latest.revision: "13"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: a0ecb0ea00a9ae5438657943e65d3bfcea635872
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="connecting-to-mysql-mysqltosql"></a>连接到 MySQL (MySQLToSQL)
若要将 MySQL 数据库迁移到 SQL Server 或 SQL Azure，你必须连接到你想要迁移的 MySQL 数据库。 连接时，SSMA 获取有关所有 MySQL 架构，元数据，然后在 MySQL 元数据资源管理器窗格中显示内容。 SSMA 存储有关数据库服务器的信息，但不会存储密码。  
  
数据库的连接将保持活动状态，直到关闭该项目。 当你重新打开项目时，你必须重新连接，如果你想与数据库的活动连接。  
  
有关 MySQL 数据库的元数据不自动更新。 相反，如果你想要更新 MySQL 元数据资源管理器中的元数据，则必须手动更新它。 有关详细信息，请参阅本主题后面的"刷新 MySQL 元数据"部分。  
  
## <a name="required-mysql-permissions"></a>所需的 MySQL 权限  
用于连接到 MySQL 数据库的帐户必须至少具有**连接**权限。 这使 SSMA 从连接的用户拥有的架构中获取元数据。 获取其他架构中的对象的元数据，然后转换这些架构中的对象，该帐户必须具有以下权限：  
  
-   在数据库对象上的显示权限  
  
-   选择对 Information_schema 特权  
  
-   选择 mysql 的权限 （对于 Udf)  
  
## <a name="establishing-a-connection-to-mysql"></a>建立的连接到 MySQL  
当你连接到数据库时，SSMA 读取数据库元数据，然后将此元数据添加到项目文件。 当它将对象转换为 SQL Server 或 SQL Azure 的语法，以及它将数据迁移到 SQL Server 或 SQL Azure，将通过 SSMA 使用此元数据。 你可以浏览此元数据在 MySQL 元数据资源管理器窗格中，并检查各个数据库对象的属性。  
  
> [!IMPORTANT]  
> 你尝试进行连接之前，请确保数据库服务器正在运行，并且可以接受连接。  
  
**若要连接到 MySQL**  
  
1.  上**文件**菜单上，选择**连接到 MySQL** （在项目的创建之后将启用此选项）。  
  
    如果你以前连接到 MySQL，命令名称将**重新连接到 MySQL**。  
  
2.  在**提供程序**框中，选择 MySQL ODBC 5.1 驱动程序 （受信任）。 它是默认的提供程序在标准模式下。  
  
3.  在**模式**框中，选择**标准模式**。 它是默认模式。  
  
    使用标准的模式来指定服务器名称和端口。  
  
4.  在**标准模式**，提供以下值：  
  
    1.  在**服务器名称**框中，输入 MySQL 服务器名称。 在**服务器端口**框中，输入端口号为 3306。 它是默认端口。  
  
    2.  在**用户名**框中，输入 MySQL 帐户具有所需的权限。  
  
    3.  在**密码**框中，指定的用户名称中输入的密码。  
  
5.  **SSL:**如果你想要安全地连接到 MySQL，请通过检查使用的安全套接字层 (SSL) **SSL**复选框。  
  
6.  **配置：**它提供一个选项以配置 MySQL 通过安全套接字层 (SSL) 的连接。  
  
    > [!NOTE]  
    > 若要启用**配置**，SSL 必须设置为**True**。  
  
    单击"配置"按钮，会出现一个对话框。 若要使用加密，而必须连接到 MySQL 数据库，对以下三个证书文件在对话框中存在的路径定义 [隐私增强邮件证书 (PEM)]:  
  
    -   **SSL 证书颁发机构：**的信任 SSL Ca 的列表中指定文件的路径。  
  
    -   **SSL 证书：**指定要用于建立安全连接使用的 SSL 证书文件的名称。  
  
    -   **SSL 密钥：**指定 SSL 密钥文件用于建立的安全连接的名称。  
  
    > [!NOTE]  
    > -   **确定**按钮启用时提供了所需的信息。 如果任何文件路径无效，"确定"按钮将一直保持禁用。  
    > -   **取消**按钮关闭对话框并**关闭**主连接窗体中的 SSL 选项。  
  
7.  有关详细信息，请参阅[连接到 MySQL &#40;MySQLToSQL &#41;](../../ssma/mysql/connect-to-mysql-mysqltosql.md)  
  
## <a name="reconnecting-to-mysql"></a>重新连接到 MySQL  
与数据库服务器的连接将保持活动状态，直到关闭该项目。 当你重新打开项目时，你必须重新连接，如果你想与数据库的活动连接。 你想要更新元数据，加载到 SQL Server 或 SQL Azure 的数据库对象，迁移数据之前，你可以脱机工作。  
  
## <a name="refreshing-mysql-metadata"></a>正在刷新 MySQL 元数据  
有关 MySQL 数据库的元数据不会自动刷新。 MySQL 元数据资源管理器中的元数据是首次连接时的元数据或最后一次你手动刷新元数据的快照。 你可以手动更新所有架构、 单个架构或单独的数据库对象的元数据。  
  
**若要刷新元数据**  
  
1.  请确保你已连接到数据库。  
  
2.  在 MySQL 元数据资源管理器，选择你想要更新每个架构或数据库对象旁边的复选框。  
  
3.  右键单击**架构**，或单个架构或数据库对象，，然后选择**从数据库刷新**。  
  
    如果没有活动连接，将显示 SSMA**连接到 MySQL**对话框中，因此您可以连接。  
  
4.  在从数据库对话框刷新中，指定要刷新的对象。  
  
    -   若要刷新的对象，请单击**Active**字段旁边的对象之前会出现一个箭头。  
  
    -   若要防止对象被刷新，请单击**Active**字段旁边的对象，直到**X**显示。  
  
    -   若要刷新或拒绝的对象的类别，请单击**Active**字段旁边的类别文件夹。  
  
    -   若要查看的颜色编码定义，请单击**图例**按钮。  
  
5.  单击 **“确定”**。  
  
## <a name="next-step"></a>下一步  
迁移过程的下一步是[连接到 SQL Server &#40;MySQLToSQL &#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
## <a name="see-also"></a>另请参阅  
[将 MySQL 数据库迁移到 SQL Server 的 Azure SQL DB &#40;MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
