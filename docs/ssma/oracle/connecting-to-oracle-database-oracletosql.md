---
title: 正在连接到 Oracle Database （OracleToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Refreshing Oracle Metadata
ms.assetid: e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: fc25c36a0d0133975414f4c7270da2974b552f40
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68266190"
---
# <a name="connecting-to-oracle-database-oracletosql"></a>连接到 Oracle Database (OracleToSQL)
若要将 Oracle 数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]迁移到，你必须连接到要迁移的 oracle 数据库。 当你连接时，SSMA 将获取有关所有 Oracle 架构的元数据，然后在 "Oracle 元数据资源管理器" 窗格中显示它。 SSMA 存储有关数据库服务器的信息，但不存储密码。  
  
在关闭项目之前，与数据库的连接保持活动状态。 重新打开项目时，如果要连接到数据库，则必须重新连接。  
  
有关 Oracle 数据库的元数据不会自动更新。 相反，如果要更新 Oracle 元数据资源管理器中的元数据，则必须手动对其进行更新。 有关详细信息，请参阅本主题后面的 "刷新 Oracle 元数据" 一节。  
  
## <a name="required-oracle-permissions"></a>必需的 Oracle 权限  
用于连接到 Oracle 数据库的帐户必须至少具有**connect**权限。 这使 SSMA 可以从连接用户所拥有的架构中获取元数据。 若要获取其他架构中的对象的元数据，然后转换这些架构中的对象，该帐户必须具有以下权限：  
  
-   创建任何过程  
  
-   执行任何过程  
  
-   选择任何表  
  
-   选择任意序列  
  
-   创建任意类型  
  
-   创建任何触发器  
  
-   选择任何字典  
  
## <a name="establishing-a-connection-to-oracle"></a>建立与 Oracle 的连接  
连接到数据库时，SSMA 将读取数据库元数据，然后将此元数据添加到项目文件。 当 SSMA 将对象转换为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]语法以及将其迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时，将使用此元数据。 您可以在 "Oracle 元数据资源管理器" 窗格中浏览此元数据，查看各个数据库对象的属性。  
  
> [!IMPORTANT]  
> 尝试连接之前，请确保数据库服务器正在运行，并且可以接受连接。  
  
**连接到 Oracle**  
  
1.  在 "**文件**" 菜单上，选择 "**连接到 Oracle**"。  
  
    如果以前已连接到 Oracle，则命令名称将**重新连接到 oracle**。  
  
2.  根据安装的提供程序，在 "**提供程序**" 框中选择 " **Oracle 客户端提供程序**" 或 " **OLE DB 提供程序**"。 默认值为 "Oracle 客户端"。  
  
3.  在 "**模式**" 框中，选择 "**标准模式**"、" **TNSNAME 模式**" 或 "**连接字符串模式**"。  
  
    使用 "标准" 模式指定服务器名称和端口。 使用服务名称模式手动指定 Oracle 服务名称。 使用连接字符串模式提供完整的连接字符串。  
  
4.  如果选择 "**标准" 模式**，请提供以下值：  
  
    1.  在 "**服务器名称**" 框中，输入或选择数据库服务器的名称或 IP 地址。  
  
    2.  如果数据库服务器未配置为接受默认端口（1521）上的连接，请在 "**服务器端口**" 框中输入用于 Oracle 连接的端口号。  
  
    3.  在 " **ORACLE SID** " 框中，输入系统标识符。  
  
    4.  在 "**用户名**" 框中，输入具有所需权限的 Oracle 帐户。  
  
    5.  在 "**密码**" 框中，输入指定用户名的密码。  
  
5.  如果选择**TNSNAME 模式**，请提供以下值：  
  
    1.  在 "**连接标识符**" 框中，输入数据库的连接标识符（TNS 别名）。  
  
    2.  在 "**用户名**" 框中，输入具有所需权限的 Oracle 帐户。  
  
    3.  在 "**密码**" 框中，输入指定用户名的密码。  
  
6.  如果选择 "**连接字符串模式**"，请在 "**连接字符串**" 框中提供连接字符串。  
  
    下面的示例演示一个 OLE DB 连接字符串：  
  
    `Provider=OraOLEDB.Oracle;Data Source=MyOracleDB;User Id=myUsername;Password=myPassword;`  
  
    下面的示例演示了使用集成安全性的 Oracle 客户端连接字符串：  
  
    `Data Source=MyOracleDB;Integrated Security=yes;`  
  
    有关详细信息，请参阅[连接到 Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md)。  
  
## <a name="reconnecting-to-oracle"></a>重新连接到 Oracle  
与数据库服务器的连接会一直保持活动状态，直到关闭该项目。 重新打开项目时，如果要连接到数据库，则必须重新连接。 你可以脱机工作，直至你要更新元数据、将数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]加载到和迁移数据。  
  
## <a name="refreshing-oracle-metadata"></a>刷新 Oracle 元数据  
有关 Oracle 数据库的元数据不会自动刷新。 Oracle 元数据资源管理器中的元数据是首次连接时或上次手动刷新元数据时的元数据的快照。 可以手动更新所有架构、单个架构或单个数据库对象的元数据。  
  
**刷新元数据**  
  
1.  请确保已连接到数据库。  
  
2.  在 Oracle 元数据资源管理器中，选中要更新的每个架构或数据库对象旁边的复选框。  
  
3.  右键单击 "**架构**"、单个架构或数据库对象，然后选择 "**从数据库刷新**"。  
  
    如果没有活动连接，SSMA 将显示 "**连接到 Oracle** " 对话框，以便你可以连接。  
  
4.  在 "从数据库刷新" 对话框中，指定要刷新的对象。  
  
    -   若要刷新对象，请单击对象旁边的**活动**字段，直到出现箭头。  
  
    -   若要防止对象被刷新，请单击对象旁边的**活动**字段，直到出现**X** 。  
  
    -   若要刷新或拒绝某个对象类别，请单击 "category" 文件夹旁边的**活动**字段。  
  
    若要查看颜色编码的定义，请单击 "**图例**" 按钮。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="next-step"></a>下一步  
  
-   迁移过程的下一步是[连接到 SQL Server 的实例](connecting-to-sql-server-oracletosql.md)。  
  
## <a name="see-also"></a>另请参阅  
[将 Oracle 数据库迁移到 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
