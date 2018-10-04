---
title: 连接到 MySQL (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to MySQL, MySQL permission
- Connecting to MySQL,reconnecting
ms.assetid: 084c7020-f729-4f91-90e0-143f85fa68d1
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 638a79e5785c74a11cb2e424739c3d80959a4d40
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47843075"
---
# <a name="connecting-to-mysql-mysqltosql"></a>连接到 MySQL (MySQLToSQL)
若要将 MySQL 数据库迁移到 SQL Server 或 SQL Azure，必须连接到你想要迁移的 MySQL 数据库。 连接时，SSMA 中获取有关所有 MySQL 架构的元数据，然后在 MySQL 的元数据资源管理器窗格中显示。 SSMA 存储信息，数据库服务器中，但不存储密码。  
  
与数据库的连接保持活动状态，直到关闭该项目。 重新打开该项目，必须重新连接如果想要的活动连接到数据库。  
  
有关 MySQL 数据库的元数据不会自动更新。 相反，如果你想要更新 MySQL 元数据资源管理器中的元数据，则必须手动更新它。 有关详细信息，请参阅本主题后面的"刷新 MySQL 元数据"部分。  
  
## <a name="required-mysql-permissions"></a>所需的 MySQL 的权限  
用于连接到 MySQL 数据库的帐户必须至少具有**CONNECT**权限。 这使 SSMA 从连接的用户拥有的架构中获取元数据。 若要获取的其他架构中的对象元数据，然后将转换这些架构中的对象，该帐户必须具有以下权限：  
  
-   对数据库对象的显示特权  
  
-   在 SELECT 特权 Information_schema  
  
-   选择 mysql 特权 （Udf)  
  
## <a name="establishing-a-connection-to-mysql"></a>与 MySQL 建立连接  
当连接到数据库时，SSMA 读取数据库元数据，然后将此元数据添加到项目文件。 将对象转换为 SQL Server 或 SQL Azure 的语法，以及它将数据迁移到 SQL Server 或 SQL Azure，SSMA 使用此元数据。 您可以浏览此 MySQL 元数据资源管理器窗格中的元数据，并查看单独的数据库对象的属性。  
  
> [!IMPORTANT]  
> 尝试连接之前，请确保数据库服务器正在运行，并且可以接受连接。  
  
**若要连接到 MySQL**  
  
1.  上**文件**菜单中，选择**连接到 MySQL** （项目创建后会启用此选项）。  
  
    如果您以前连接到 MySQL，命令名称将是**重新连接到 MySQL**。  
  
2.  在中**提供程序**框中，选择 MySQL ODBC 5.1 驱动程序 （受信任）。 它是在标准模式下的默认提供程序。  
  
3.  在中**模式下**框中，选择**标准模式**。 它是默认模式。  
  
    使用标准模式来指定服务器名称和端口。  
  
4.  在中**标准模式**，提供以下值：  
  
    1.  在中**服务器名称**框中，输入 MySQL 服务器名称。 在中**服务器端口**框中，输入端口号为 3306。 它是默认端口。  
  
    2.  在中**用户名**框中，输入 MySQL 帐户具有所需的权限。  
  
    3.  在**密码**框中，输入指定的用户名的密码。  
  
5.  **SSL:** 如果你想要安全地连接到 MySQL，请使用安全套接字层 (SSL) 通过检查**SSL**复选框。  
  
6.  **配置：** 它提供了一个选项以配置 MySQL 通过安全套接字层 (SSL) 连接。  
  
    > [!NOTE]  
    > 若要启用**配置**，SSL 必须设置为**True**。  
  
    在单击"配置"按钮，会出现一个对话框。 若要使用加密，而连接到 MySQL 数据库，以下三个证书中的文件的对话框中的路径必须被定义 [隐私增强邮件证书 (PEM)]:  
  
    -   **SSL 证书颁发机构：** 信任 SSL Ca 的一系列指定文件的路径。  
  
    -   **SSL 证书：** 指定要用于建立安全连接的 SSL 证书文件的名称。  
  
    -   **SSL 密钥：** 指定要用于建立安全连接的 SSL 密钥文件的名称。  
  
    > [!NOTE]  
    > -   **确定**按钮已启用时提供了所需的信息。 如果任何文件路径无效，"确定"按钮将保持禁用状态。  
    > -   **取消**按钮关闭对话框和**将关闭**主连接窗体中的 SSL 选项。  
  
7.  有关详细信息，请参阅[连接到 MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connect-to-mysql-mysqltosql.md)  
  
## <a name="reconnecting-to-mysql"></a>重新连接到 MySQL  
与数据库服务器的连接将保持活动状态，直到您关闭该项目。 重新打开该项目，必须重新连接如果想要的活动连接到数据库。 你想要更新元数据、 数据库对象加载到 SQL Server 或 SQL Azure，并将数据迁移前，您可以脱机工作。  
  
## <a name="refreshing-mysql-metadata"></a>正在刷新 MySQL 元数据  
有关 MySQL 数据库的元数据不会自动刷新。 MySQL 元数据资源管理器中的元数据是首次连接时的元数据或上一次在手动刷新元数据的快照。 您可以手动更新所有架构、 单一架构或单独的数据库对象的元数据。  
  
**若要刷新元数据**  
  
1.  请确保您已连接到数据库。  
  
2.  在 MySQL 的元数据资源管理器，选择你想要更新每个架构或数据库对象旁边的复选框。  
  
3.  用鼠标右键单击**架构**，或者单个架构或数据库对象，然后再选择**从数据库刷新**。  
  
    如果没有活动连接，将显示 SSMA**连接到 MySQL**对话框中，以便可以连接。  
  
4.  在刷新数据库对话框中，指定要刷新的对象。  
  
    -   若要刷新对象，请单击**活动**字段旁边会显示一个箭头，直到该对象。  
  
    -   若要禁止刷新对象，请单击**活动**字段相邻的对象，直到**X**出现。  
  
    -   若要刷新或拒绝的对象类别，请单击**活动**类别文件夹旁边的字段。  
  
    -   若要查看的颜色代码定义，请单击**图例**按钮。  
  
5.  单击“确定” 。  
  
## <a name="next-step"></a>下一步  
迁移过程中的下一步是[连接到 SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
## <a name="see-also"></a>请参阅  
[迁移 MySQL 数据库移到 SQL Server-Azure SQL 数据库&#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
