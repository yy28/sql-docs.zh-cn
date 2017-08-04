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
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b2a5deb6e6ec95e6f6707abe9ad85374b2334e05
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

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
> 你可能需要下载并安装其他要连接到你选择的访问的版本的文件。 请参阅[获取所需连接到 Access 文件](#officeDownloads)本页了解详细信息。

如果您指定了版本时遇到问题，请尝试指定不同的版本，甚至早期版本。 例如，你可能无法安装 Office 2016 数据提供程序，因为你有 Microsoft Office 365 订阅。 只能使用桌面版本的 Microsoft Office 安装的数据提供程序访问 2016年和 Excel 2016。 在这种情况下，你可以指定 Access 2013，而不是访问 2016年。 两个版本的提供程序在功能上等效。 中提到了 Office 2016 运行时的这一局限性[这篇博客文章](https://blogs.office.com/2015/12/16/access-2016-runtime-is-now-available-for-download/)。

 **File name**  
指定访问文件的路径和文件名称。 例如， **c:\\MyData.mdb**的本地计算机上的文件或** \\\\销售\\数据库\\Northwind.mdb**网络共享上的文件。 或单击 **“浏览”**。 

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
  
## <a name="officeDownloads"></a>获取所需连接到 Access 文件  
你可能需要下载 Microsoft Office 数据源，包括 Excel 和访问权限，如果它们尚未安装连接组件。

更高版本的组件可以打开早期版本的程序所创建的文件。 在许多情况下，早期版本的组件也可以打开的程序的更高版本创建的文件。 例如，如果你不能安装 Office 2016 组件，请改用 Office 2013 组件。 两个版本的提供程序在功能上等效。 中提到了 Office 2016 运行时的这一局限性[这篇博客文章](https://blogs.office.com/2015/12/16/access-2016-runtime-is-now-available-for-download/)。

如果计算机具有 Office 的 32 位版本-这是正常现象，即使在 64 位计算机-然后你必须安装 32 位版本的组件。 你还必须确保在运行 32 位向导中，或运行该向导在 32 位模式下创建的 SQL Server Integration Services 包。

|Microsoft Office 版本|下载|  
|------------------------------|--------------|  
|2016|[Microsoft Access 2016 Runtime](https://www.microsoft.com/download/details.aspx?id=50040)|
|2013|[Microsoft Access 2013 Runtime](http://www.microsoft.com/download/details.aspx?id=39358)|
|2010|[Microsoft Access 2010 Runtime](https://www.microsoft.com/download/details.aspx?id=10910)|  
|2007|[2007 Office System Driver: Data Connectivity Components（Office 2007 系统驱动程序：数据连接组件）](https://www.microsoft.com/download/details.aspx?id=23734)|    

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


