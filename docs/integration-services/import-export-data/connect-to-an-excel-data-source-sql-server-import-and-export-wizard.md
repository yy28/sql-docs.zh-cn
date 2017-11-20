---
title: "连接到 Excel 数据源 （SQL Server 导入和导出向导） |Microsoft 文档"
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
ms.assetid: 43fbaca0-36d8-4583-9056-af7010209b87
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: b4411fdd2337d93f15b149febf845fb7b0762c40
ms.contentlocale: zh-cn
ms.lasthandoff: 08/28/2017

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
> 你可能需要下载并安装其他要连接到 Excel 文件的文件。 请参阅[获取所需连接到 Excel 文件](#officeDownloads)本页了解详细信息。

**首行包含列名称**  
指示数据的第一行是否包含列名称。
-   如果数据不包含列名称，但你启用此选项，则向导将源数据的第一行作为列名称。
-   如果数据包含列名称，但禁用此选项，向导会将列名称的行视为数据的第一行。

如果你指定的数据不具有列名，则向导将 F1，F2，依此类推，使用作为列标题。

## <a name="i-dont-see-excel-in-the-list-of-data-sources"></a>我看不到 Excel 中的数据源列表
如果你看不到 Excel 中的数据源列表，你在运行 64 位向导？ 有关 Excel 和 Access 的提供程序是通常是 32 位和 64 位向导中不可见。 请改为运行 32 位向导。

> [!NOTE]
> 若要使用 64 位版本的 SQL Server 导入和导出向导，你必须安装 SQL Server。 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS) 是 32 位应用程序，仅安装 32 位文件，包括 32 位版本的向导。

## <a name="officeDownloads"></a>获取所需连接到 Excel 文件  
你可能需要下载 Microsoft Office 数据源，包括 Excel 和访问权限，如果它们尚未安装连接组件。 下载最新版本的 Excel 和 Access 文件此处连接组件： [Microsoft Access 数据库引擎 2016年可再发行组件](https://www.microsoft.com/download/details.aspx?id=54920)。
  
组件的最新版本可以打开的 Excel 的早期版本创建的文件。

如果计算机具有 32 位版本的 Office，那么您需要安装 32 位版本的组件，并还需要确保在 32 位模式下运行包。

如果你有 Office 365 订阅，请确保你下载访问数据库引擎 2016年可再发行组件和不是 Microsoft 访问 2016年运行时。 运行安装程序时，可能会看到一条错误消息，您无法下载通过并行安装 Office 单击以运行组件。 要绕过此错误消息，请运行安装程序在静默模式下打开命令提示符窗口并运行。使用下载的 EXE 文件`/quiet`切换。 例如：

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="see-also"></a>另请参阅
[选择数据源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[选择目标](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


