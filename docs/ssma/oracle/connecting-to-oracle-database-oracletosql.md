---
title: 连接到 Oracle 数据库 (OracleToSQL) |Microsoft 文档
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Refreshing Oracle Metadata
ms.assetid: e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 93814b7d1b40a14d76dbc2548c128f382131d98e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-to-oracle-database-oracletosql"></a>连接到 Oracle 数据库 (OracleToSQL)
若要迁移到的 Oracle 数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，你必须连接到你想要迁移的 Oracle 数据库。 连接时，SSMA 获取有关所有 Oracle 架构，元数据，然后在 Oracle 元数据资源管理器窗格中显示内容。 SSMA 存储有关数据库服务器的信息，但不会存储密码。  
  
数据库的连接将保持活动状态，直到关闭该项目。 当你重新打开项目时，你必须重新连接，如果你想与数据库的活动连接。  
  
有关 Oracle 数据库的元数据不自动更新。 相反，如果你想要更新 Oracle 元数据资源管理器中的元数据，则必须手动更新它。 有关详细信息，请参阅本主题后面的"刷新 Oracle 元数据"部分。  
  
## <a name="required-oracle-permissions"></a>必需的 Oracle 权限  
用于连接到 Oracle 数据库的帐户必须至少具有**连接**权限。 这使 SSMA 从连接的用户拥有的架构中获取元数据。 获取其他架构中的对象的元数据，然后转换这些架构中的对象，该帐户必须具有以下权限：  
  
-   创建任何过程  
  
-   执行任何过程  
  
-   选择任何表  
  
-   选择任何序列  
  
-   创建任何类型  
  
-   CREATE ANY TRIGGER  
  
-   选择任何字典  
  
## <a name="establishing-a-connection-to-oracle"></a>建立与 Oracle 的连接  
当你连接到数据库时，SSMA 读取数据库元数据，然后将此元数据添加到项目文件。 此元数据转换到的对象时，SSMA 使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]语法中，当它迁移到的数据和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 你可以浏览此元数据在 Oracle 元数据资源管理器窗格中，并检查各个数据库对象的属性。  
  
> [!IMPORTANT]  
> 你尝试进行连接之前，请确保数据库服务器正在运行，并且可以接受连接。  
  
**若要连接到 Oracle**  
  
1.  上**文件**菜单上，选择**连接到 Oracle**。  
  
    如果你以前连接到 Oracle，命令名称将**重新连接到 Oracle**。  
  
2.  在**提供程序**框中，选择**Oracle 客户端提供程序**或**OLE DB 访问接口**，取决于安装的提供程序。 默认值为 Oracle 客户端。  
  
3.  在**模式**框中，选择**标准模式**， **TNSNAME 模式**，或**连接字符串模式**。  
  
    使用标准的模式来指定服务器名称和端口。 使用服务名称模式，若要手动指定 Oracle 服务名称。 使用连接字符串模式来提供完整连接字符串。  
  
4.  如果你选择**标准模式**，提供以下值：  
  
    1.  在**服务器名称**框中，输入或选择的名称或数据库服务器的 IP 地址。  
  
    2.  如果数据库服务器未配置为接受连接上的默认端口 (1521)，请输入中的 Oracle 连接使用的端口号**服务器端口**框。  
  
    3.  在**Oracle SID**框中，输入的系统标识符。  
  
    4.  在**用户名**框中，输入具有所需的权限的 Oracle 帐户。  
  
    5.  在**密码**框中，指定的用户名称中输入的密码。  
  
5.  如果你选择**TNSNAME 模式**，提供以下值：  
  
    1.  在**连接标识符**框中，输入连接的数据库的标识符 （TNS 别名）。  
  
    2.  在**用户名**框中，输入具有所需的权限的 Oracle 帐户。  
  
    3.  在**密码**框中，指定的用户名称中输入的密码。  
  
6.  如果你选择**连接字符串模式**，提供连接字符串中的**连接字符串**框。  
  
    下面的示例演示一个 OLE DB 连接字符串：  
  
    `Provider=OraOLEDB.Oracle;Data Source=MyOracleDB;User Id=myUsername;Password=myPassword;`  
  
    下面的示例演示一个使用集成的安全性的 Oracle 客户端连接字符串：  
  
    `Data Source=MyOracleDB;Integrated Security=yes;`  
  
    有关详细信息，请参阅[连接到 Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md)。  
  
## <a name="reconnecting-to-oracle"></a>重新连接到 Oracle  
与数据库服务器的连接将保持活动状态，直到关闭该项目。 当你重新打开项目时，你必须重新连接，如果你想与数据库的活动连接。 您可以离线工作之前你想要更新元数据，数据库将对象加载到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，并迁移数据。  
  
## <a name="refreshing-oracle-metadata"></a>正在刷新 Oracle 元数据  
有关 Oracle 数据库的元数据不会自动刷新。 Oracle 元数据资源管理器中的元数据是首次连接时的元数据或最后一次你手动刷新元数据的快照。 你可以手动更新所有架构、 单个架构或单独的数据库对象的元数据。  
  
**若要刷新元数据**  
  
1.  请确保你已连接到数据库。  
  
2.  在 Oracle 元数据资源管理器，选择你想要更新每个架构或数据库对象旁边的复选框。  
  
3.  右键单击**架构**，或单个架构或数据库对象，，然后选择**从数据库刷新**。  
  
    如果没有活动连接，将显示 SSMA**连接到 Oracle**对话框中，因此您可以连接。  
  
4.  在从数据库对话框刷新中，指定要刷新的对象。  
  
    -   若要刷新的对象，请单击**Active**字段旁边的对象之前会出现一个箭头。  
  
    -   若要防止对象被刷新，请单击**Active**字段旁边的对象，直到**X**显示。  
  
    -   若要刷新或拒绝的对象的类别，请单击**Active**字段旁边的类别文件夹。  
  
    若要查看的颜色编码定义，请单击**图例**按钮。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok_md.md)]  
  
## <a name="next-step"></a>下一步  
  
-   迁移过程的下一步是[连接到的 SQL Server 实例](http://msdn.microsoft.com/en-us/1b2a8059-1829-4904-a82f-9c06de1e245f)。  
  
## <a name="see-also"></a>另请参阅  
[迁移的 Oracle 数据库移到 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
