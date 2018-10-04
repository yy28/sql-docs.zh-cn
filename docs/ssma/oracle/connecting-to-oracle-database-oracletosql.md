---
title: 连接到 Oracle 数据库 (OracleToSQL) |Microsoft Docs
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
manager: v-thobro
ms.openlocfilehash: 4ad868122fd8986c642bace1b2c9cf419bb89182
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47634325"
---
# <a name="connecting-to-oracle-database-oracletosql"></a>连接到 Oracle Database (OracleToSQL)
将 Oracle 数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，必须连接到你想要迁移的 Oracle 数据库。 连接时，SSMA 中获取有关所有 Oracle 架构的元数据，然后在 Oracle 元数据资源管理器窗格中显示。 SSMA 存储信息，数据库服务器中，但不存储密码。  
  
与数据库的连接保持活动状态，直到关闭该项目。 重新打开该项目，必须重新连接如果想要的活动连接到数据库。  
  
有关 Oracle 数据库的元数据不会自动更新。 相反，如果你想要更新 Oracle 元数据资源管理器中的元数据，则必须手动更新它。 有关详细信息，请参阅本主题后面的"刷新 Oracle 元数据"部分。  
  
## <a name="required-oracle-permissions"></a>所需的 Oracle 权限  
用于连接到 Oracle 数据库的帐户必须至少具有**CONNECT**权限。 这使 SSMA 从连接的用户拥有的架构中获取元数据。 若要获取的其他架构中的对象元数据，然后将转换这些架构中的对象，该帐户必须具有以下权限：  
  
-   创建任何过程  
  
-   执行任何过程  
  
-   选择任何表  
  
-   选择任何序列  
  
-   创建任何类型  
  
-   创建任何触发器  
  
-   选择任何字典  
  
## <a name="establishing-a-connection-to-oracle"></a>建立与 Oracle 的连接  
当连接到数据库时，SSMA 读取数据库元数据，然后将此元数据添加到项目文件。 它将转换到的对象时，使用此元数据的 SSMA[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]语法，并当它会将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 您可以浏览 Oracle 元数据资源管理器窗格中的此元数据，并查看单独的数据库对象的属性。  
  
> [!IMPORTANT]  
> 尝试连接之前，请确保数据库服务器正在运行，并且可以接受连接。  
  
**若要连接到 Oracle**  
  
1.  上**文件**菜单中，选择**连接到 Oracle**。  
  
    如果你之前连接到 Oracle，命令名称将是**重新连接到 Oracle**。  
  
2.  在中**提供程序**框中，选择**Oracle 客户端提供程序**或**OLE DB 访问接口**，取决于安装的提供程序。 默认值是 Oracle 客户端。  
  
3.  在**模式下**框中，选择**标准模式**， **TNSNAME 模式**，或者**连接字符串模式**。  
  
    使用标准模式来指定服务器名称和端口。 使用服务名称模式，若要手动指定 Oracle 服务名称。 使用连接字符串模式来提供完整的连接字符串。  
  
4.  如果您选择**标准模式**，提供下列值：  
  
    1.  在**服务器名称**框中，输入或选择的名称或 IP 地址数据库服务器。  
  
    2.  如果数据库服务器未配置为接受连接在默认端口 (1521) 中，输入用于中的 Oracle 连接的端口号**服务器端口**框。  
  
    3.  在中**Oracle SID**框中，输入系统标识符。  
  
    4.  在中**用户名**框中，输入 Oracle 帐户具有所需的权限。  
  
    5.  在**密码**框中，输入指定的用户名的密码。  
  
5.  如果选择**TNSNAME 模式**，提供以下值：  
  
    1.  在中**连接标识符**框中，输入连接的数据库的标识符 （TNS 别名）。  
  
    2.  在中**用户名**框中，输入 Oracle 帐户具有所需的权限。  
  
    3.  在**密码**框中，输入指定的用户名的密码。  
  
6.  如果选择**连接字符串模式**，提供连接字符串**连接字符串**框。  
  
    下面的示例演示的 OLE DB 连接字符串：  
  
    `Provider=OraOLEDB.Oracle;Data Source=MyOracleDB;User Id=myUsername;Password=myPassword;`  
  
    下面的示例显示了使用集成的安全性的 Oracle 客户端连接字符串：  
  
    `Data Source=MyOracleDB;Integrated Security=yes;`  
  
    有关详细信息，请参阅[连接到 Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md)。  
  
## <a name="reconnecting-to-oracle"></a>重新连接到 Oracle  
与数据库服务器的连接将保持活动状态，直到您关闭该项目。 重新打开该项目，必须重新连接如果想要的活动连接到数据库。 您可以脱机处理直到您要更新元数据，加载到数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，和迁移数据。  
  
## <a name="refreshing-oracle-metadata"></a>正在刷新 Oracle 元数据  
Oracle 数据库的元数据不会自动刷新。 Oracle 的元数据资源管理器中的元数据是元数据，当您首次连接或上次您手动刷新元数据的快照。 您可以手动更新所有架构、 单一架构或单独的数据库对象的元数据。  
  
**若要刷新元数据**  
  
1.  请确保您已连接到数据库。  
  
2.  在 Oracle 的元数据资源管理器中，选择您要更新的每个架构或数据库对象旁边的复选框。  
  
3.  用鼠标右键单击**架构**，或者单个架构或数据库对象，然后再选择**从数据库刷新**。  
  
    如果没有活动的连接，将显示 SSMA**连接到 Oracle**对话框，以便您可以连接。  
  
4.  在刷新数据库对话框中，指定要刷新的对象。  
  
    -   若要刷新对象，请单击**活动**字段旁边会显示一个箭头，直到该对象。  
  
    -   若要禁止刷新对象，请单击**活动**字段相邻的对象，直到**X**出现。  
  
    -   若要刷新或拒绝的对象类别，请单击**活动**类别文件夹旁边的字段。  
  
    若要查看的颜色代码定义，请单击**图例**按钮。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="next-step"></a>下一步  
  
-   迁移过程的下一步是为[连接到的 SQL Server 实例](connecting-to-sql-server-oracletosql.md)。  
  
## <a name="see-also"></a>请参阅  
[迁移的 Oracle 数据库移到 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
