---
title: "连接到 ODBC 数据源 （SQL Server 导入和导出向导） |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e6318776-a188-48a7-995d-9eafd7148ff2
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 0e3ffe2ff1695de69be7149f4be7b42f57b0e991
ms.contentlocale: zh-cn
ms.lasthandoff: 08/28/2017

---
# <a name="connect-to-an-odbc-data-source-sql-server-import-and-export-wizard"></a>连接到 ODBC 数据源 （SQL Server 导入和导出向导）
本主题演示如何连接到**ODBC**数据源从**选择数据源**或**选择目标**SQL Server 导入和导出向导中的页。

你可能需要下载 ODBC 驱动程序需要从 Microsoft 或从第三方。

你可能还需要查找你必须提供所需的连接信息。 此第三方站点-[该连接字符串引用](https://www.connectionstrings.com/)-包含示例连接字符串和有关数据提供程序的详细信息和它们需要的连接信息。

## <a name="make-sure-the-driver-you-want-is-installed"></a>请确保你想安装的驱动程序
1.  搜索或浏览到**ODBC 数据源 （64 位）**控制面板中的小程序。 如果你只有 32 位驱动程序，或你知道，你必须使用 32 位驱动程序，搜索或浏览到**ODBC 数据源 （32 位）**相反。
2.  启动控制面板小程序。 **ODBC 数据源管理器**窗口随即打开。
3.  上**驱动程序**选项卡上，你可以找到在计算机上安装的所有 ODBC 驱动程序的列表。 （某些驱动程序的名称可能列出多个语言版本。）

    下面是已安装 64 位驱动程序列表中的示例。

    ![已安装 64 位 ODBC 驱动程序](../../integration-services/import-export-data/media/installed-64-bit-odbc-drivers.png)

> [!TIP]
> 如果您知道驱动程序的安装，并且你未看到它在 64 位控制面板小程序中，查找在 32 位控制面板小程序相反。 这还将告知你是否可以运行的 64 位或 32 位 SQL Server 导入和导出向导。
>
> 若要使用 64 位版本的 SQL Server 导入和导出向导，你必须安装 SQL Server。 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS) 是 32 位应用程序，仅安装 32 位文件，包括 32 位版本的向导。
    
## <a name="step-1---select-the-data-source"></a>步骤 1-选择数据源
在计算机上安装的 ODBC 驱动程序未列出在下拉列表中的数据源。 若要连接使用 ODBC 驱动程序，首先要选择**适用于 ODBC 的.NET Framework 数据提供程序**上的数据源作为**选择数据源**或**选择目标**向导页。 此提供程序充当 ODBC 驱动程序周围的包装器。

这是在选择用于 ODBC 的.NET Framework 数据提供程序之后立即看到泛型屏幕。

![连接到与之前的 ODBC SQL](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-before.jpg)

## <a name="step-2---provide-the-connection-info"></a>步骤 2-提供连接信息
下一步是为 ODBC 驱动程序和数据源提供的连接信息。 您有两种选择：
1.  提供**DSN** （数据源名称） 已存在，或创建具有**ODBC 数据源管理器**控制面板中的小程序。 DSN 是所需连接到 ODBC 数据源的设置已保存的集合。

    如果你已知道 DSN 名称，或了解如何创建新的 DSN 现在，你可以跳过此页的其余部分。 输入中的 DSN 名称**Dsn**字段上**选择数据源**或**选择目标**页上，则继续执行向导的下一步。

    [提供一个 DSN](#odbc_dsn)
    
2.  提供**连接字符串**，你可以查找联机状态，或创建和测试与计算机上的**ODBC 数据源管理器**小程序。

    如果你已有的连接字符串，或了解如何创建它，则可以跳过此页的其余部分。 输入中的连接字符串**ConnectionString**字段上**选择数据源**或**选择目标**页上，则继续执行向导的下一步。

    [提供连接字符串](#odbc_connstring)

如果你提供连接字符串，**选择数据源**或**选择目标**页显示向导要用于连接到您的数据源，例如，服务器和数据库的名称和身份验证方法的所有连接信息。 如果你提供一个 DSN，则此信息不可见。

## <a name="odbc_dsn"></a>选项 1-提供 DSN
如果你想要提供与 DSN （数据源名称） 的连接信息，请使用**ODBC 数据源管理器**小程序，以找到相应名称的现有 DSN，或创建新的 DSN。
1.  搜索或浏览到**ODBC 数据源 （64 位）**控制面板中的小程序。 如果你仅有 32 位驱动程序，或必须使用 32 位驱动程序，搜索或浏览到**ODBC 数据源 （32 位）**相反。
2.  启动控制面板小程序。 **ODBC 数据源管理器**窗口随即打开。 下面是小程序的外观。

    ![ODBC 管理器控制面板小程序](../../integration-services/import-export-data/media/odbc-administrator-control-panel-applet.png)
    
3.  如果你想要**使用现有 DSN**对于数据源时，你可以使用你在看到任何 DSN**用户 DSN**，**系统 DSN**，或**文件 DSN**选项卡。请检查名称，然后返回到向导中输入它**Dsn**字段上**选择数据源**或**选择目标**页。 跳过此页的其余部分并继续在向导的下一步。
4.  如果你想要**创建的新 DSN**、 决定是否希望其成为可见仅对你 (用户 DSN) 对计算机的所有用户可见包括 Windows 服务 （系统 DSN），或保存在文件 (File DSN)。 此示例将创建新的系统 DSN。
5. 上**系统 DSN**选项卡上，单击**添加**。

    ![添加新的 ODBC 系统 DSN](../../integration-services/import-export-data/media/add-a-new-odbc-system-dsn.png)
    
6.  在**创建新的数据源**对话框中，选择数据源时，驱动程序，然后单击**完成**。

    ![选取驱动程序作为新系统 DSN](../../integration-services/import-export-data/media/pick-driver-for-new-system-dsn.png)
    
7. 该驱动程序现在将显示你在其中输入连接到数据源所需的信息的一个或多个特定于驱动程序的屏幕。 （对于 SQL Server 驱动程序，例如，有四个页面的自定义设置。）在完成后，新的系统 DSN 出现在列表中。

    ![列表中的新系统 DSN](../../integration-services/import-export-data/media/new-system-dsn-in-list.png)
    
8.  返回到向导并输入中的 DSN 名称**Dsn**字段上**选择数据源**或**选择目标**页。 继续向导的下一步。

## <a name="odbc_connstring"></a>选项 2-提供连接字符串
如果你想要提供你的连接信息与连接字符串，本主题的其余部分可帮助你获取所需的连接字符串。

此示例将使用以下连接字符串，连接到 Microsoft SQL Server。

    Driver={ODBC Driver 13 for SQL Server};server=localhost;database=WideWorldImporters;trusted_connection=Yes;

输入中的连接字符串**ConnectionString**字段上**选择数据源**或**选择目标**页。 输入连接字符串后，向导将分析字符串，并在列表中显示的各个属性及其值。

下面是你输入的连接字符串后看到的屏幕。

![连接到使用 ODBC 后的 SQL](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

> [!NOTE]
> 是否要配置你的源或目标，ODBC 驱动程序的连接选项都是相同的。 你看到的选项，即是上都相同**选择数据源**和**选择目标**向导页。

## <a name="get-the-connection-string-online"></a>获取连接字符串
若要查找 ODBC 驱动程序连接字符串，请参阅[该连接字符串引用](https://www.connectionstrings.com/)。 此第三方站点包含示例连接字符串以及有关数据提供程序的详细信息和它们需要的连接信息。

## <a name="get-the-connection-string-with-an-app"></a>获取与应用的连接字符串
若要生成并测试你在你自己的计算机上的 ODBC 驱动程序的连接字符串，你可以使用**ODBC 数据源管理器**控制面板中的小程序。 创建你的连接，文件 DSN，然后复制文件 DSN 来组合的连接字符串外的设置。 这需要几个步骤，但有助于确保具有有效的连接字符串。

1.  搜索或浏览到**ODBC 数据源 （64 位）**控制面板中的小程序。 如果你仅有 32 位驱动程序，或必须使用 32 位驱动程序，搜索或浏览到**ODBC 数据源 （32 位）**相反。
2.  启动控制面板小程序。 **ODBC 数据源管理器**窗口随即打开。
3.  现在请转到**文件 DSN**选项卡上的小程序。 单击 **“添加”**。

    对于此示例中，创建文件 DSN 而不是用户 DSN 或系统 DSN，因为文件 DSN 将名称 / 值对保存在连接字符串所需的特定格式。

    ![添加新的 ODBC 文件 DSN](../../integration-services/import-export-data/media/add-a-new-odbc-file-dsn.png)

4.  在**新建数据源**对话框中，在列表中，选择您的驱动程序，然后单击**下一步**。 此示例将创建包含我们需要连接到 Microsoft SQL Server 的连接字符串自变量的 DSN。

    ![创建新的 ODBC 数据源](../../integration-services/import-export-data/media/create-new-odbc-data-source.png)
    
5.  选择一个位置并输入新的文件 DSN 的文件名，然后单击**下一步**。 请记住，因此你可以找到它并打开在后续步骤中保存该文件。

    ![保存新文件 DSN](../../integration-services/import-export-data/media/save-new-file-dsn.png)

6.  查看你选择的摘要，然后单击**完成**。

7.  单击后**完成**，你选择的驱动程序将显示一个或多个专有的屏幕，以收集它需要将其连接的信息。 通常此信息包括服务器、 登录信息和基于服务器的数据源和文件、 格式和版本的基于文件的数据源的数据库。

8. 配置您的数据源并单击后**完成**，你通常查看你的选择的摘要，并有机会对其进行测试。

    ![测试新文件 DSN](../../integration-services/import-export-data/media/test-new-file-dsn.png)

9. 测试您的数据源并关闭对话框后，查找文件系统中的你保存文件 DSN。 如果你未更改的文件扩展名，则默认扩展名是。DSN。

10. 使用记事本或其他文本编辑器中打开保存的文件。 以下是我们的 SQL Server 示例内容。

        [ODBC]  
        DRIVER=ODBC Driver 13 for SQL Server  
        TrustServerCertificate=No  
        DATABASE=WideWorldImporters    
        WSID=<local computer name>  
        APP=Microsoft® Windows® Operating System  
        Trusted_Connection=Yes  
        SERVER=localhost   
        
11. 复制并粘贴到用分号分隔的名称-值对的连接字符串的所需的值。

    从示例文件 DSN 组合所需值后，你将具有以下连接字符串。
    
        DRIVER=ODBC Driver 13 for SQL Server;SERVER=localhost;DATABASE=WideWorldImporters;Trusted_Connection=Yes

    您通常不需要创建通过 ODBC 数据源管理器创建的连接字符串的工作原理的 DSN 中的所有设置。  
    -   你始终必须指定的 ODBC 驱动程序。
    -   对于类似于 SQL Server 基于服务器的数据源，您通常需要服务器、 数据库和登录信息。 因此在示例 DSN 中，你无需再 TrustServerCertificate、 WSID 或应用程序。
    -   对于基于文件的数据源，需要至少文件名称和位置。
    
12. 粘贴到此连接字符串**ConnectionString**字段上**选择数据源**或**选择目标**向导页。 向导将分析字符串，并且你已准备好继续 ！

    ![连接到使用 ODBC 后的 SQL](../../integration-services/import-export-data/media/connect-to-sql-with-odbc-after.jpg)

## <a name="see-also"></a>另请参阅
[选择数据源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[选择目标](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)



