---
title: 连接到 ODBC 数据源（SQL Server 导入和导出向导）| Microsoft Docs
description: 介绍如何配置 ODBC DSN 或创建用于 SQL Server 导入和导出向导的 ODBC 连接字符串
ms.custom: ''
ms.date: 06/29/2020
ms.prod: sql
ms.reviewer: vanto
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e6318776-a188-48a7-995d-9eafd7148ff2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a4049581b36d05f178fc56fa37bf332bfc2355a2
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917091"
---
# <a name="connect-to-an-odbc-data-source-sql-server-import-and-export-wizard"></a>连接到 ODBC 数据源（SQL Server 导入和导出向导）

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


本主题介绍如何从 SQL Server 导入和导出向导的“选择数据源”页或“选择目标”页连接到 ODBC 数据源    。

可能需要从 Microsoft 或第三方下载所需的 ODBC 驱动程序。

可能还需要查找必须提供的连接信息。 第三方站点 - [The Connection Strings Reference（连接字符串参考）](https://www.connectionstrings.com/) - 包含示例连接字符串、关于数据提供程序的详细信息及它们需要的连接信息。

## <a name="make-sure-the-driver-you-want-is-installed"></a>确保已安装所需驱动程序
1.  在开始菜单或控制面板中搜索或浏览到“ODBC 数据源 (64 位)”小程序  。 如果只有 32 位驱动程序，或了解必须使用 32 位驱动程序，请改为搜索或浏览到“ODBC 数据源(32 位)”  。
2.  启动小程序。 此时会打开“ODBC 数据源管理器”窗口  。
3.  在“驱动程序”选项卡上，可找到计算机上安装的所有 OBDC 驱动程序的列表  。 （部分驱动程序的名称可能以多个语言列出。）

    下面是已安装的 64 位驱动程序的示例列表。

    ![已安装的 64 位 ODBC 驱动程序](../../integration-services/import-export-data/media/installed-64-bit-odbc-drivers.png)

> [!TIP]
> 如果知晓安装了驱动程序但在 64 位小程序中未看到它，请改为在 32 位小程序中查找。 通过这种方法可同时获知是需要运行 64 位还是 32 位 SQL Server 导入和导出向导。
>
> 若要使用 64 位版本的 SQL Server 导入和导出向导，必须安装 SQL Server。 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS) 是 32 位应用程序且仅安装 32 位文件，包括 32 位版本的向导。
    
## <a name="step-1---select-the-data-source"></a>步骤 1 - 选择数据源
计算机上安装的 ODBC 驱动程序不在数据源下拉列表中列出。 要使用 ODBC 驱动程序进行连接，请首先在向导的“选择数据源”页或“选择目标”页上选择“用于 ODBC 的 .NET Framework 数据提供程序”作为数据源    。 此提供程序充当 ODBC 驱动程序的包装器。

下面是选择用于 ODBC 的 .NET Framework 数据提供程序后随即显示的常规屏幕。

![先使用 ODBC 连接到 SQL](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

## <a name="step-2---provide-the-connection-info"></a>步骤 2 - 提供连接信息
下一步是为 ODBC 驱动程序和数据源提供连接信息。 您有两种选择：
1.  提供已经存在的 DSN（数据源名称），或使用“ODBC 数据源管理器”小程序创建的 DSN   。 DSN 是连接 ODBC 数据源时所需的设置（已保存）的集合。

    如果已知 DSN 名称或已知如何创建新的 DSN，可跳过本页的其余部分。 在“选择数据源”页或“选择目标”页上的“DSN”字段中输入 DSN 名称，然后继续执行向导的下一步    。

    [提供 DSN](#odbc_dsn)
    
2.  提供一个字符串，可在计算机上使用“ODBC 数据源管理器”小程序联机查看或创建和测试该字符串   。

    如果已有连接字符串或知道如何创建，可跳过本页的其余部分。 在“选择数据源”页或“选择目标”页上的“ConnectionString”字段中输入连接字符串，然后继续执行向导的下一步    。

    [提供一个连接字符串](#odbc_connstring)

如果提供连接字符串，“选择数据源”或“选择目标”页将显示向导连接到数据源要使用的所有连接信息，例如服务器、数据库名称和身份验证方法   。 如果提供 DSN，此信息不可见。

## <a name="option-1---provide-a-dsn"></a><a name="odbc_dsn"></a>选项 1 - 提供 DSN
如果要在连接信息中提供 DSN（数据源名称），使用“ODBC 数据源管理器”小程序，查找现有 DSN 的名称或创建一个新 DSN  。
1.  在开始菜单或控制面板中搜索或浏览到“ODBC 数据源 (64 位)”小程序  。 如果只有 32 位驱动程序，或必须使用 32 位驱动程序，请改为搜索或浏览到“ODBC 数据源(32 位)”  。
2.  启动小程序。 此时会打开“ODBC 数据源管理器”窗口  。 下面是小程序的外观。

    ![ODBC 管理器控制面板小程序](../../integration-services/import-export-data/media/odbc-administrator-control-panel-applet.png)
    
3.  如果要对数据源使用现有 DSN，可以使用“用户 DSN”、“系统 DSN”或“文件 DSN”选项卡上显示的任何 DSN     。检查名称，然后返回向导，在“选择数据源”页或“选择目标”页上的“DSN”字段中输入该名称    。 跳过本页的其余部分并继续执行向导的下一步。
4.  如果要创建新 DSN，请确定是只对自己可见（用户 DSN）、对包含 Windows 服务的计算机的所有用户可见（系统 DSN）还是将其保存在文件中（文件 DSN）  。 此示例创建一个新的系统 DSN。
5. 在“系统 DSN”选项卡上，单击“添加”   。

    ![添加新的 ODBC 系统 DSN](../../integration-services/import-export-data/media/add-a-new-odbc-system-dsn.png)
    
6.  在“新建数据源”对话框中，选择数据源的驱动程序，然后单击“完成”   。

    ![为新系统 DSN 选取驱动程序](../../integration-services/import-export-data/media/pick-driver-for-new-system-dsn.png)
    
7. 驱动程序现在显示一个或多个驱动程序专用的屏幕，可在其中输入连接数据源所需的信息。 （例如，对于 SQL Server 驱动程序，自定义设置有 4 页。）完成后，新的系统 DSN 将出现在列表中。

    ![列表中的新系统 DSN](../../integration-services/import-export-data/media/new-system-dsn-in-list.png)
    
8.  返回向导，在“选择数据源”页或“选择目标”页上的“DSN”字段中输入 DSN 名称    。 继续执行向导的下一步。

## <a name="option-2---provide-a-connection-string"></a><a name="odbc_connstring"></a>选项 2 - 提供一个连接字符串
如果要在连接信息中提供连接字符串，可借助本主题的其余内容获取所需的连接字符串。

本示例将使用以下连接字符串，该字符串与 Microsoft SQL Server 连接。 使用的数据库示例是 WideWorldImporters，我们将连接到本地计算机上的 SQL Server  。

```console
Driver={ODBC Driver 13 for SQL Server};server=localhost;database=WideWorldImporters;trusted_connection=Yes;
```

在“选择数据源”页或“选择目标”页上的“ConnectionString”字段中输入连接字符串    。 输入连接字符串后，向导会分析该字符串，并在列表中显示各个属性及其值。

下面是输入连接字符串后出现的屏幕。

![之后使用 ODBC 连接到 SQL](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

> [!NOTE]
> 不管是配置源还是目标，ODBC 驱动程序的连接选项都相同。 也就是说，在向导的“选择数据源”页和“选择目标”页上看到的选项是相同的   。

## <a name="get-the-connection-string-online"></a>联机获取连接字符串
要联机为 ODBC 驱动程序查找连接字符串，请参阅[连接字符串参考](https://www.connectionstrings.com/)。 该第三方站点包含示例连接字符串、关于数据提供程序的详细信息以及它们需要的连接信息。

## <a name="get-the-connection-string-with-an-app"></a>使用应用获取连接字符串
若要在自己的计算机上生成并测试用于 ODBC 驱动程序的连接字符串，可以使用“控制面板”中的“ODBC 数据源管理器”小程序  。 为连接创建一个文件 DSN，然后将设置从文件 DSN 复制出来，组合成连接字符串。 这需要执行多个步骤，但有助于确保连接字符串有效。

1.  在开始菜单或控制面板中搜索或浏览到“ODBC 数据源 (64 位)”小程序  。 如果只有 32 位驱动程序，或必须使用 32 位驱动程序，请改为搜索或浏览到“ODBC 数据源(32 位)”  。
2.  启动小程序。 此时会打开“ODBC 数据源管理器”窗口  。
3.  现在，转到小程序的“文件 DSN”选项卡  。 单击“添加”  。

    对于本示例，创建文件 DSN 而不是用户 DSN 或系统 DSN，因为文件 DSN 会以连接字符串所需的特定格式来保存名称-值对。

    ![添加新的 ODBC 文件 DSN](../../integration-services/import-export-data/media/add-a-new-odbc-file-dsn.png)

4.  在“新建数据源”对话框中，选择列表中的驱动程序，然后单击“下一步”   。 此示例会创建一个 DSN，其中包含连接 Microsoft SQL Server 时所需的连接字符串参数。

    ![新建 ODBC 数据源](../../integration-services/import-export-data/media/create-new-odbc-data-source.png)
    
5.  选择一个位置并为新文件 DSN 输入文件名，然后单击“下一步”  。 请记住文件的保存位置，以便在后续步骤中可查找并打开文件。

    ![保存新文件 DSN](../../integration-services/import-export-data/media/save-new-file-dsn.png)

6.  检查所选内容的摘要，然后单击“完成”  。

7.  单击“完成”后，所选驱动程序将显示一个或多个专用屏幕，以收集连接时所需信息  。 通常，该信息包含基于服务器的数据源的服务器、登录信息和数据库，以及基于文件的数据源的文件、格式和版本。

8. 配置数据源并单击“完成”后，通常会看到所选内容的摘要，并有机会对其进行测试  。

    ![测试新文件 DSN](../../integration-services/import-export-data/media/test-new-file-dsn.png)

9. 测试数据源并关闭对话框后，在文件系统中文件 DSN 的保存位置查找它。 如果未更改文件扩展名，默认扩展名为 .DSN。

10. 使用记事本或其他文本编辑器打开保存的文件。 以下是 SQL Server 示例的内容。

    ```console
    [ODBC]  
    DRIVER=ODBC Driver 13 for SQL Server  
    TrustServerCertificate=No  
    DATABASE=WideWorldImporters    
    WSID=<local computer name>  
    APP=MicrosoftÂ® WindowsÂ® Operating System  
    Trusted_Connection=Yes  
    SERVER=localhost   
    ```
        
11. 将必需的值复制并粘贴到连接字符串中，其中使用分号分隔名称-值对。

    将示例文件 DSN 中必需的值进行组合后，会得到下面的连接字符串。
    
    ```console
    DRIVER=ODBC Driver 13 for SQL Server;SERVER=localhost;DATABASE=WideWorldImporters;Trusted_Connection=Yes
    ```

    通常无需用到 ODBC 数据源管理器创建的 DSN 中的全部设置，即可创建正常运行的连接字符串。  
    -   始终需要指定 ODBC 驱动程序。
    -   对于 SQL Server 这类基于服务器的数据源，通常需要服务器、数据库和登录信息。 在示例 DSN 中，不需要 TrustServerCertificate、WSID 或 APP。
    -   对于基于文件的数据源，至少需要文件名和位置。
    
12. 在向导“选择数据源”页或“选择目标”页上的“ConnectionString”字段中粘贴此连接字符串    。 向导会分析字符串，可继续操作！

    ![之后使用 ODBC 连接到 SQL](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

## <a name="see-also"></a>另请参阅
[选择数据源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[选择目标](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


