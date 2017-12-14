---
title: "连接到 Excel 数据源（SQL Server 导入和导出向导）| Microsoft Docs"
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 43fbaca0-36d8-4583-9056-af7010209b87
caps.latest.revision: "12"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2aeb225037970b8a77169db18c204ecf6d4c19d6
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="connect-to-an-excel-data-source-sql-server-import-and-export-wizard"></a>连接到 Excel 数据源（SQL Server 导入和导出向导）
本主题介绍如何从 SQL Server 导入和导出向导的“选择数据源”页或“选择目标”页连接到 **Microsoft Excel** 数据源。

下面的屏幕截图显示到 Microsoft Excel 工作簿的示例连接。

![Excel 连接](../../integration-services/import-export-data/media/excel-connection.png) 

## <a name="options-to-specify"></a>要指定的选项

> [!NOTE]
> 无论 Excel 是源还是目标，此数据提供程序的连接选项都相同。 也就是说，在向导的“选择数据源”页和“选择目标”页上看到的选项是相同的。

**Excel 文件路径**  
 指定 Excel 文件的路径和文件名。 例如：
-   针对本地计算机上的文件，指定 **C:\\MyData.xlsx**。
-   针对网络共享上的文件，指定 **\\\\Sales\\Database\\Northwind.xlsx**。

或单击 **“浏览”**。  
  
 **浏览**  
 通过使用“打开”对话框定位电子表格。  

> [!NOTE]
> 该向导无法打开受密码保护的 Excel 文件。

 **Excel 版本**  
选择源工作簿使用的 Excel 版本。

> [!IMPORTANT]
> 可能需要下载并安装其他文件，才能连接到 Excel 文件。 有关详细信息，请参阅本页的[获取连接到 Excel 所需的文件](#officeDownloads)。

**首行包含列名称**  
指示数据的首行是否包含列名称。
-   如果数据不包含列名称，但启用了此选项，则向导会将源数据的首行作为列名称。
-   如果数据包含列名称，但禁用了此选项，则向导会将列名称一行作为数据的首行。

如果指定数据不具有列名称，则向导会使用 F1、F2 等作为列标题。

## <a name="i-dont-see-excel-in-the-list-of-data-sources"></a>我在数据源列表中看不到 Excel
如果在数据源列表中看不到 Excel，你运行的是 64 位向导？ Excel 和 Access 的提供程序通常是 32 位，在 64 位向导中不会显示。 请改为运行 32 位向导。

> [!NOTE]
> 若要使用 64 位版本的 SQL Server 导入和导出向导，必须安装 SQL Server。 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS) 是 32 位应用程序且仅安装 32 位文件，包括 32 位版本的向导。

## <a name="officeDownloads"></a>获取连接到 Excel 所需的文件  
如果尚未安装 Microsoft Office 数据源（包括 Excel 和 Access）的连接组件，则可能需要下载它们。 在 [Microsoft Access 2016 数据库引擎可再发行（程序包）](https://www.microsoft.com/download/details.aspx?id=54920)中为 Excel 和 Access 文件下载最新版本的连接组件。
  
最新版组件可以打开 Excel 早期版本创建的文件。

如果计算机有 32 位版本的 Office，则必须安装 32 位版本的组件，并且还必须确保在 32 位模式下运行包。

如果有 Office 365 订阅，请确保下载 Access 数据库引擎 2016 可再发行组件，而不是 Microsoft Access 2016 Runtime。 运行安装程序时，可能会看到一条错误消息，指出该下载项无法与 Office 即点即用组件并行安装。 若要绕过此错误消息，请打开命令提示符窗口并使用 `/quiet` 开关运行下载的 .EXE 文件，从而在安静模式下运行安装。 例如：

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="see-also"></a>另请参阅
[选择数据源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[选择目标](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

