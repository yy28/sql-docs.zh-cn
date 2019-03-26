---
title: 连接到 Excel 数据源（SQL Server 导入和导出向导）| Microsoft Docs
ms.custom: ''
ms.date: 04/02/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 43fbaca0-36d8-4583-9056-af7010209b87
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e91a32da57488153e9d916cb70232d64c9b38a1b
ms.sourcegitcommit: 5683044d87f16200888eda2c2c4dee38ff87793f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2019
ms.locfileid: "58221811"
---
# <a name="connect-to-an-excel-data-source-sql-server-import-and-export-wizard"></a>连接到 Excel 数据源（SQL Server 导入和导出向导）
本文介绍如何从 SQL Server 导入和导出向导的“选择数据源”页或“选择目标”页连接到 Microsoft Excel 数据源。

下面的屏幕截图显示到 Microsoft Excel 工作簿的示例连接。

![Excel 连接](../../integration-services/import-export-data/media/excel-connection.png) 

可能需要下载并安装其他文件，才能连接到 Excel 文件。 有关详细信息，请参阅[获取连接到 Excel 所需的文件](../load-data-to-from-excel-with-ssis.md#files-you-need)。

> [!IMPORTANT]
> 有关连接到 Excel 文件的详细信息，以及从 Excel 文件加载数据或将数据加载到 Excel 文件的限制和已知问题，请参阅[使用 SQL Server Integration Services (SSIS) 从 Excel 加载数据或将数据加载到 Excel 中](../load-data-to-from-excel-with-ssis.md)。

## <a name="options-to-specify"></a>要指定的选项

> [!NOTE]
> 无论 Excel 是源还是目标，此数据提供程序的连接选项都相同。 也就是说，在向导的“选择数据源”页和“选择目标”页上看到的选项是相同的。

**Excel 文件路径**  
 指定 Excel 文件的路径和文件名。 例如：
-   针对本地计算机上的文件，指定 **C:\\MyData.xlsx**。
-   针对网络共享上的文件，指定 **\\\\Sales\\Database\\Northwind.xlsx**。

或单击 **“浏览”**。  
  
 **“浏览”**  
 通过使用“打开”对话框定位电子表格。  

> [!NOTE]
> 该向导无法打开受密码保护的 Excel 文件。

 **Excel 版本**  
选择源或目标工作簿使用的 Excel 版本。

**首行包含列名称**  
指示数据的首行是否包含列名称。
-   如果数据不包含列名称，但启用了此选项，则向导会将源数据的首行作为列名称。
-   如果数据包含列名称，但禁用了此选项，则向导会将列名称一行作为数据的首行。

如果指定数据不具有列名称，则向导会使用 F1、F2 等作为列标题。

## <a name="i-dont-see-excel-in-the-list-of-data-sources"></a>我在数据源列表中看不到 Excel
如果在数据源列表中看不到 Excel，你运行的是 64 位向导？ Excel 和 Access 的提供程序通常是 32 位，在 64 位向导中不会显示。 请改为运行 32 位向导。

> [!NOTE]
> 若要使用 64 位版本的 SQL Server 导入和导出向导，必须安装 SQL Server。 SQL Server Data Tools (SSDT) 和 SQL Server Management Studio (SSMS) 是 32 位应用程序且仅安装 32 位文件，包括 32 位版本的向导。

## <a name="see-also"></a>另请参阅
[使用 SQL Server Integration Services (SSIS) 从 Excel 加载数据或将数据加载到 Excel 中](../load-data-to-from-excel-with-ssis.md)  
[选择数据源](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[选择目标](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

