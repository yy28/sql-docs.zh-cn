---
title: "连接到 Access 数据源 （SQL Server 导入和导出向导） |Microsoft 文档"
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b44c159a-c33d-4f3c-bdb8-9832f35317c8
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 71bb3914e31259bc95a1116c2db03708c0442e8c
ms.contentlocale: zh-cn
ms.lasthandoff: 08/28/2017

---
# <a name="connect-to-an-access-data-source-sql-server-import-and-export-wizard"></a>连接到 Access 数据源 （SQL Server 导入和导出向导）
本主题演示如何连接到**Microsoft Access**数据源从**选择数据源**或**选择目标**SQL Server 导入和导出向导中的页。

下面的屏幕截图显示到 Microsoft Access 数据库的示例连接。 在此示例中，你无需输入用户名和密码，因为目标数据库不使用工作组信息文件。

![连接到 Access](../../integration-services/import-export-data/media/connect-to-access.jpg)

## <a name="options-to-specify"></a>若要指定的选项

> [!NOTE]
> 无论访问是你的源或目标，此数据提供程序的连接选项都是相同。 你看到的选项，即是上都相同**选择数据源**和**选择目标**向导页。

**数据源**  
Microsoft Access 数据提供程序的列表可能包含多个条目。 选择最新的安装的版本或到创建数据库文件的访问的版本相对应的版本。

|数据源|Office 版本|
|-------|-------|
|Microsoft Access (Microsoft.ACE.OLEDB.16.0)|Office 2016|
|Microsoft Access (Microsoft.ACE.OLEDB.15.0)|Office 2013|
|Microsoft Access （Microsoft Access 数据库引擎）|Office 2010 和 Office 2007|
|Microsoft Access （Microsoft Jet 数据库引擎）|早于 Office 2007 office 版本|

> [!IMPORTANT]
> 你可能需要下载并安装其他要连接到 Access 数据库文件。 请参阅[获取所需连接到 Access 文件](#officeDownloads)本页了解详细信息。

 **File name**  
指定访问文件的路径和文件名称。 例如， **c:\\MyData.mdb**的本地计算机上的文件或 **\\\\销售\\数据库\\Northwind.mdb**网络共享上的文件。 或单击 **“浏览”**。 

 >   [!NOTE] 
 > 如果你单击**浏览**查找访问文件，**打开**对话框框中使用较旧的文件的筛选器。默认情况下 MDB 格式和文件扩展名。 但是该数据提供程序还可打开文件与较新。ACCDB 格式和文件扩展名。
  
 **浏览**  
 通过使用“打开”对话框定位数据库文件。  
  
 **用户名**  
如果工作组信息文件与数据库关联，请提供有效的用户名。  
  
 **密码**  
如果工作组信息文件与数据库关联，请提供用户的密码。
 
如果使用的所有用户一个密码保护数据库，请参阅[是数据库文件受密码保护？](#database_password)。
  
 **高级**  
在中指定高级的选项，例如数据库密码或非默认工作组信息文件，**数据链接属性**对话框。  

## <a name="i-dont-see-access-in-the-list-of-data-sources"></a>数据源的列表中看不到访问
如果你看不到访问的数据源列表中，你在运行 64 位向导？ 有关 Excel 和 Access 的提供程序是通常是 32 位和 64 位向导中不可见。 请改为运行 32 位向导。

> [!NOTE]
> 若要使用 64 位版本的 SQL Server 导入和导出向导，你必须安装 SQL Server。 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS) 是 32 位应用程序，仅安装 32 位文件，包括 32 位版本的向导。

## <a name="officeDownloads"></a>获取所需连接到 Access 文件  
你可能需要下载 Microsoft Office 数据源，包括 Access 和 Excel，如果它们尚未安装连接组件。 下载最新版本的 Access 和 Excel 文件此处连接组件： [Microsoft Access 数据库引擎 2016年可再发行组件](https://www.microsoft.com/download/details.aspx?id=54920)。
  
组件的最新版本可打开文件的访问的早期版本创建的。

如果计算机具有 32 位版本的 Office，那么您需要安装 32 位版本的组件，并还需要确保在 32 位模式下运行包。

如果你有 Office 365 订阅，请确保你下载访问数据库引擎 2016年可再发行组件和不是 Microsoft 访问 2016年运行时。 运行安装程序时，可能会看到一条错误消息，您无法下载通过并行安装 Office 单击以运行组件。 要绕过此错误消息，请运行安装程序在静默模式下打开命令提示符窗口并运行。使用下载的 EXE 文件`/quiet`切换。 例如：

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="database_password"></a>数据库文件是受密码保护？
在某些情况下，Access 数据库是受密码保护，但不使用工作组信息文件。 所有用户必须提供相同的密码，但无需输入用户名。 若要提供数据库密码，执行以下操作。

1.  上**选择数据源**或**选择目标**页上，单击**高级**按钮以打开**数据链接属性**对话框。  
2.  在**数据链接属性**对话框中，选择**所有**选项卡。  
3.  在属性值的列表中，选择**Jet OLEDB:Database 密码**。   
    
    ![指定访问密码，屏幕 1](../../integration-services/import-export-data/media/specify-access-password-screen-1.jpg) 
4.  单击**编辑值**以打开**编辑属性值**对话框。  
    
    ![指定访问密码，屏幕 2](../../integration-services/import-export-data/media/specify-access-password-screen-2.jpg)
5.  在**编辑属性值**对话框框中，输入数据库密码。
6.  单击**确定**在每个对话框中，以返回到**选择数据源**或**选择目标**向导页面并继续。

## <a name="keep-your-autonumber-values-when-you-export-from-access"></a>从访问导出时保留你 autonumber 值
若要允许在要插入到目标表中的标识列的源数据中使用现有的标识值，选择**启用标识插入**选项**列映射**对话框。 默认情况下，对目标标识列通常不可以将现有值插入。 若要显示**列映射**对话框中，选择**编辑映射**在访问**选择源表和源视图**向导页。 若要查看这些页面，请参阅[选择源表和源视图](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)和[列映射](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)。

如果现有主键位于标识列、自动编号列或等效列中，则通常必须选择此选项以保留现有主键值。 否则目标标识列通常会分配新值。

## <a name="see-also"></a>另请参阅
[选择数据源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[选择目标](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


