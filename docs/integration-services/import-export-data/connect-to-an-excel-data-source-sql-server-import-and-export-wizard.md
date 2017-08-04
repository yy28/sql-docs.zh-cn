---
title: "连接到 Excel 数据源 （SQL Server 导入和导出向导） |Microsoft 文档"
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 43fbaca0-36d8-4583-9056-af7010209b87
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d744e84aa2b4ae0462a5d5a1e4453a9e86abb890
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-an-excel-data-source-sql-server-import-and-export-wizard"></a>连接到 Excel 数据源 （SQL Server 导入和导出向导）
本主题演示如何连接到**Microsoft Excel**数据源从**选择数据源**或**选择目标**SQL Server 导入和导出向导中的页。

下面的屏幕截图显示到 Microsoft Excel 工作簿的示例连接。

![Excel 连接](../../integration-services/import-export-data/media/excel-connection.png) 

## <a name="options-to-specify"></a>若要指定的选项

> [!NOTE]
> Excel 是否您的源或目标，此数据提供程序的连接选项都是相同的。 你看到的选项，即是上都相同**选择数据源**和**选择目标**向导页。

**Excel 文件路径**  
 指定 Excel 文件路径和文件名。 例如：
-   本地计算机上的文件**c:\\MyData.xlsx**。
-   网络共享上的文件 **\\\\销售\\数据库\\Northwind.xlsx**。

或单击 **“浏览”**。  
  
 **浏览**  
 通过使用“打开”对话框定位电子表格。  

> [!NOTE]
> 该向导无法打开受密码保护的 Excel 文件。

 **Excel 版本**  
选择源工作簿使用的 Excel 版本。

> [!IMPORTANT]
> 可能需要下载并安装其他文件，才能连接到所选 Excel 版本。 请参阅[获取所需连接到 Excel 文件](#officeDownloads)本页了解详细信息。

如果您指定了版本时遇到问题，请尝试指定不同的版本，甚至早期版本。 例如，你可能无法安装 Office 2016 数据提供程序，因为你有 Microsoft Office 365 订阅。 只能使用桌面版本的 Microsoft Office 安装的数据提供程序访问 2016年和 Excel 2016。 在这种情况下，你可以指定 Excel 2013，而不是 Excel 2016。 两个版本的提供程序在功能上等效。 中提到了 Office 2016 运行时的这一局限性[这篇博客文章](https://blogs.office.com/2015/12/16/access-2016-runtime-is-now-available-for-download/)。

**首行包含列名称**  
指示数据的第一行是否包含列名称。
-   如果数据不包含列名称，但你启用此选项，则向导将源数据的第一行作为列名称。
-   如果数据包含列名称，但禁用此选项，向导会将列名称的行视为数据的第一行。

如果你指定的数据不具有列名，则向导将 F1，F2，依此类推，使用作为列标题。

## <a name="i-dont-see-excel-in-the-list-of-data-sources"></a>我看不到 Excel 中的数据源列表
如果你看不到 Excel 中的数据源列表，你在运行 64 位向导？ 有关 Excel 和 Access 的提供程序是通常是 32 位和 64 位向导中不可见。 请改为运行 32 位向导。

## <a name="officeDownloads"></a>获取所需连接到 Excel 文件  
你可能需要下载 Microsoft Office 数据源，包括 Excel 和访问权限，如果它们尚未安装连接组件。

更高版本的组件可以打开早期版本的程序所创建的文件。 在某些情况下，早期版本的组件也可以打开程序的更高版本所创建的文件。 例如，如果你不能安装 Office 2016 组件，请改用 Office 2013 组件。 两个版本的提供程序在功能上等效。 中提到了 Office 2016 运行时的这一局限性[这篇博客文章](https://blogs.office.com/2015/12/16/access-2016-runtime-is-now-available-for-download/)。

如果计算机具有 Office 的 32 位版本-这是正常现象，即使在 64 位计算机-然后你必须安装 32 位版本的组件。 你还必须确保在运行 32 位向导中，或运行该向导在 32 位模式下创建的 SQL Server Integration Services 包。 
 
|Microsoft Office 版本|下载|  
|------------------------------|--------------|  
|2016|[Microsoft Access 2016 Runtime](https://www.microsoft.com/download/details.aspx?id=50040)|
|2013|[Microsoft Access 2013 Runtime](http://www.microsoft.com/download/details.aspx?id=39358)|
|2010|[Microsoft Access 2010 Runtime](https://www.microsoft.com/download/details.aspx?id=10910)|  
|2007|[2007 Office System Driver: Data Connectivity Components（Office 2007 系统驱动程序：数据连接组件）](https://www.microsoft.com/download/details.aspx?id=23734)|  

## <a name="see-also"></a>另请参阅
[选择数据源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[选择目标](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


