---
title: "连接到 Access 数据源（SQL Server 导入和导出向导）| Microsoft Docs"
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b44c159a-c33d-4f3c-bdb8-9832f35317c8
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e3217fe03497c2d72f3ce0a2c321df5e089ce4e1
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="connect-to-an-access-data-source-sql-server-import-and-export-wizard"></a>连接到 Access 数据源（SQL Server 导入和导出向导）
本主题介绍如何从 SQL Server 导入和导出向导的“选择数据源”页或“选择目标”页连接到 **Microsoft Access** 数据源。

下面的屏幕截图显示到 Microsoft Access 数据库的示例连接。 在此示例中，无需输入用户名和密码，因为目标数据库不使用工作组信息文件。

![连接到 Access](../../integration-services/import-export-data/media/connect-to-access.jpg)

## <a name="options-to-specify"></a>要指定的选项

> [!NOTE]
> 无论 Access 是源还是目标，此数据提供程序的连接选项都相同。 也就是说，在向导的“选择数据源”页和“选择目标”页上看到的选项是相同的。

**数据源**  
数据提供程序列表可能包含有关 Microsoft Access 的多个条目。 请选择最新安装的版本，或与创建数据库文件的 Access 版本相对应的版本。

|数据源|Office 版本|
|-------|-------|
|Microsoft Access (Microsoft.ACE.OLEDB.16.0)|Office 2016|
|Microsoft Access (Microsoft.ACE.OLEDB.15.0)|Office 2013|
|Microsoft Access（Microsoft Access 数据库引擎）|Office 2010 和 Office 2007|
|Microsoft Access（Microsoft Jet 数据库引擎）|Office 2007 以前的 Office 版本|

> [!IMPORTANT]
> 可能需要下载并安装其他文件，才能连接到 Access 数据库。 有关详细信息，请参阅本页的[获取连接到 Access 所需的文件](#officeDownloads)。

 **文件名**  
指定 Access 文件的路径和文件名。 例如，针对本地计算机上的文件，指定 **C:\\MyData.mdb**；针对网络共享上的文件，指定 **\\\\Sales\\Database\\Northwind.mdb**。 或单击 **“浏览”**。 

 >   [!NOTE] 
 > 如果单击“浏览”定位 Access 文件，默认情况下，“打开”对话框会筛选出使用较旧 .MDB 格式和文件扩展名的文件。 不过，该数据提供程序也可以打开使用较新 .ACCDB 格式和文件扩展名的文件。
  
 **“浏览”**  
 通过使用“打开”对话框定位数据库文件。  
  
 **User name**  
如果工作组信息文件与数据库关联，则提供一个有效的用户名。  
  
 **密码**  
如果工作组信息文件与数据库关联，则在此处提供用户密码。
 
如果针对所有用户使用单个密码保护数据库，请参阅[数据库文件是否受密码保护？](#database_password)。
  
 **高级**  
在“数据链接属性”对话框中指定高级选项，比如数据库密码或非默认工作组信息文件。  

## <a name="i-dont-see-access-in-the-list-of-data-sources"></a>我在数据源列表中看不到 Access
如果在数据源列表中看不到 Access，你运行的是 64 位向导？ Excel 和 Access 的提供程序通常是 32 位，在 64 位向导中不会显示。 请改为运行 32 位向导。

> [!NOTE]
> 若要使用 64 位版本的 SQL Server 导入和导出向导，必须安装 SQL Server。 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS) 是 32 位应用程序且仅安装 32 位文件，包括 32 位版本的向导。

## <a name="officeDownloads"></a>获取连接到 Access 所需的文件  
如果尚未安装 Microsoft Office 数据源（包括 Access 和 Excel）的连接组件，则可能需要下载它们。 从此处下载 Access 和 Excel 文件的最新版连接组件：[Microsoft Access 数据库引擎 2016 可再发行组件](https://www.microsoft.com/download/details.aspx?id=54920)。
  
最新版组件可以打开 Access 早期版本创建的文件。

如果计算机有 32 位版本的 Office，则必须安装 32 位版本的组件，还须确保在 32 位模式下运行程序包。

如果有 Office 365 订阅，请确保下载 Access 数据库引擎 2016 可再发行组件，而不是 Microsoft Access 2016 Runtime。 运行安装程序时，可能会看到一条错误消息，指出该下载项无法与 Office 即点即用组件并行安装。 若要绕过此错误消息，请打开命令提示符窗口并使用 `/quiet` 开关运行下载的 .EXE 文件，从而在安静模式下运行安装。 例如：

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="database_password"></a> 数据库文件是否受密码保护？
在某些情况下，Access 数据库受密码保护，但不使用工作组信息文件。 所有用户都必须提供相同的密码，但不必输入用户名。 若要提供数据库密码，请执行以下操作。

1.  在“选择数据源”或“选择目标”页上，单击“高级”按钮打开“数据链接属性”对话框。  
2.  在“数据链接属性”对话框中，选择“全部”选项卡。  
3.  在属性和值列表中，选择“Jet OLEDB:数据库密码”。   
    
    ![指定 Access 密码，屏幕 1](../../integration-services/import-export-data/media/specify-access-password-screen-1.jpg) 
4.  单击“编辑值”打开“编辑属性值”对话框。  
    
    ![指定 Access 密码，屏幕 2](../../integration-services/import-export-data/media/specify-access-password-screen-2.jpg)
5.  在“编辑属性值”对话框中，输入数据库密码。
6.  在每个对话框中都单击“确定”，以返回到向导的“选择数据源”或“选择目标”页并继续操作。

## <a name="keep-your-autonumber-values-when-you-export-from-access"></a>从 Access 导出时保留自动编号值
若要允许将源数据中的现有标识值插入到目标表中的标识列，请选择“列映射”对话框中的“启用标识插入”选项。 默认情况下，目标标识列通常不允许用户插入现有值。 若要显示“列映射”对话框，请在到达向导的“选择源表和源视图”页时选择“编辑映射”。 若要查看这些页面，请参阅[选择源表和源视图](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md)和[列映射](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)。

如果现有主键位于标识列、自动编号列或等效列中，则通常必须选择此选项以保留现有主键值。 否则目标标识列通常会分配新值。

## <a name="see-also"></a>另请参阅
[选择数据源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[选择目标](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

