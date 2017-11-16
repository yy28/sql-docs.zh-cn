---
title: "启动 SQL Server Management Studio | Microsoft Docs"
ms.custom: 
ms.date: 07/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: 25ffaea6-0eee-4169-8dd0-1da417c28fc6
caps.latest.revision: "45"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 6fad886d9f1748a671ee206d02df1b9398bd73c3
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="lesson-1-1---start-sql-server-management-studio"></a>课程 1-1 - 启动 SQL Server Management Studio
开始本教程之前，让我们先来了解一下 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
## <a name="opening-sql-server-management-studio"></a>打开 SQL Server Management Studio  
  
#### <a name="to-open-sql-server-management-studio"></a>打开 SQL Server Management Studio  
  
1.  如何启动 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] (SSMS) 取决于操作系统。  
  * 对于具有“开始页”的较新版本的 Windows，在“开始页”中键入 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，可显示该程序。 单击该程序以打开 SSMS。 你可能想要右键单击该程序，并将其固定到“开始页”。   
  * 对于较旧版本的 Windows，在“开始”菜单上，指向“所有程序”，再指向 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]，然后单击“SQL Server Management Studio”。 或者在“运行”对话框中，键入“SSMS.exe”，然后单击“确定”。  
  
    > [!NOTE]  
    >  如果未显示 SSMS，则可能未成功安装 SSMS。 从 [下载中心](../download-sql-server-management-studio-ssms.md)安装 SSMS。 SSMS 不会随 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 自动安装。 使用最新版本访问所有功能。  
  
2.  在下一步中，使用 SSMS 的**对象资源管理器**组件连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果未显示“对象资源管理器”窗格，请在“视图”菜单上，单击“对象资源管理器”。 在“对象资源管理器”菜单上，单击“连接”按钮，再单击“数据库引擎”。 此时应显示“连接到服务器”对话框。 （如果之前已安装 SSMS，那么用户设置可能使“连接到服务器”对话框自动显示。）  
  
3.  在“连接到服务器”对话框中，完成“服务器名称”框的输入。 可以连接到三种类型的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的一个。 每种类型的“服务器名称”框的格式略有不同。 选择以下格式之一：  
  -  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的默认实例：在计算机上安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时，可将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例指定为默认实例（未命名实例）或命名实例。 如果要连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的默认实例，请插入计算机的名称。 例如，如果在名为 Accounting 的计算机上运行 SSMS，并且连接到在该计算机上安装的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的默认实例，则在“服务器名称”框中键入“Accounting”。  
  -  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的命名实例：在安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 期间，可以指定实例的名称；例如，在名为“Accounting”的计算机上，可以指定名为“Receivables”的命名实例。 若要连接到命名实例，请在“服务器名称”框中键入计算机名反斜杠实例名；例如 **Accounting\Receivables**。  
  -  **Azure SQL 数据库：**SQL 数据库的服务器名称的格式为 SQL_Server_name.database.windows.net，例如 **mydb2.database.windows.net**。 如果在为服务器命名时遇到问题，请访问 Azure 门户以获取创建连接字符串的帮助。  
  
4. 在“身份验证”区域中，选择一种身份验证方法。  
  - 如果你是计算机管理员，并且只安装了 SQL Server，请尝试使用 Windows 身份验证。  此方法也适用于配置为有权访问 SQL Server 的域用户。 由于登录尝试使用用于登录 Windows 的凭据，因此，“用户名”和“密码”框为灰显。 
  -  如果你知道用户帐户的名称和密码，请选择“SQL Server身份验证”，然后提供用户名和密码。
  - 如果你有最新版本的 SSMS，则拥有 3 个以上的选项可供选择，从“Active Directory 身份验证”开始。 有关这些更高级选项的信息，请参阅[使用 SQL 数据库和 SQL 数据仓库进行通用身份验证（MFA 的 SSMS 支持）](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-ssms-mfa-authentication)。  
  
## <a name="management-studio-components"></a>Management Studio 组件  
[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 在专用于特定信息类型的窗口中显示信息。 数据库信息显示在对象资源管理器和文档窗口中。  
  
-   对象资源管理器是服务器中所有数据库对象的树视图。 此树视图可以包括 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]和 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]的数据库。 对象资源管理器包括与其连接的所有服务器的信息。 打开 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]时，系统会提示您将对象资源管理器连接到上次使用的设置。 您可以在“已注册的服务器”组件中双击任意服务器进行连接，但无需注册要连接的服务器。  
  
-   文档窗口是 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的最大部分。 文档窗口可能包含查询编辑器和浏览器窗口。 默认情况下，将显示已与当前计算机上的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例连接的“摘要”页。  
  
## <a name="showing-additional-windows"></a>显示其他窗口  
  
#### <a name="to-show-the-registered-servers-window"></a>显示“已注册的服务器”窗口  
  
1.  在“视图”菜单上，单击“已注册的服务器”。  
  
    “已注册的服务器”窗口显示在对象资源管理器的上面或旁边。 可以将其拖放到不同的位置。 “已注册的服务器”窗口列出的是经常管理的服务器。 可以在此列表中添加和删除服务器。 列出的服务器中仅包含运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机上的 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 实例。  
  
2.  如果未显示所需的服务器，请在“已注册的服务器”中右键单击“数据库引擎”，单击“任务”，再单击“更新本地服务器注册”。 若要添加其他 SQL Server 或 SQL 数据库，请右键单击“已注册的服务器”中的某个位置，然后单击“新建服务器注册”。 完成“登录”区域，正如完成“连接到服务器”对话框。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
[与已注册的服务器和对象资源管理器连接](../../tools/sql-server-management-studio/lesson-1-2-connect-with-registered-servers-and-object-explorer.md)  

  
