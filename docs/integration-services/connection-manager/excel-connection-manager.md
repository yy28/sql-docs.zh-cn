---
title: "Excel 连接管理器 | Microsoft Docs"
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.dts.designer.excelconnection.f1
helpviewer_keywords:
- files [Integration Services], connections
- connections [Integration Services], Excel
- Excel [Integration Services]
- connection managers [Integration Services], Excel
ms.assetid: 667419f2-74fb-4b50-b963-9197d1368cda
caps.latest.revision: "41"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5785a2753b61cde59a5ed157d697b05a93796fc7
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="excel-connection-manager"></a>Excel 连接管理器
  Excel 连接管理器使包可以连接到现有的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 工作簿文件。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 所包含的 Excel 源和 Excel 目标使用 Excel 连接管理器。  
  
 将 Excel 连接管理器添加到包时， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 会创建将在运行时作为 Excel 连接进行解析的连接管理器，设置该连接管理器的属性，并将该连接管理器添加到包上的 **Connections** 集合。  
  
 该连接管理器的 **ConnectionManagerType** 属性设置为 **EXCEL**。  
  
## <a name="configuration-of-the-excel-connection-manager"></a>Excel 连接管理器的配置  
 可以按照下列方式配置 Excel 连接管理器：  
  
-   指定 Excel 工作簿文件的路径。  
  
    > [!NOTE]  
    >  无法连接到受密码保护的 Excel 文件。  
  
-   指定用于创建文件的 Excel 的版本。  
  
-   指示所选工作表或范围中的第一行被访问数据是否包含列名称。  
  
 如果 Excel 源使用 Excel 连接管理器，则被提取的数据将附带列名称。 如果 Excel 目标使用它，则列名称包括在被写入的数据中。  
  
 有关 Excel 源和 Excel 目标行为的详细信息，请参阅 [Excel Source](../../integration-services/data-flow/excel-source.md) 和 [Excel Destination](../../integration-services/data-flow/excel-destination.md)。  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请参阅 [Excel 连接管理器编辑器](../../integration-services/connection-manager/excel-connection-manager-editor.md)。  
  
 有关以编程方式配置连接管理器的信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以编程方式添加连接](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)。  
  
 有关循环遍历 Excel 文件中的某个组的信息，请参阅 [使用 Foreach 循环容器，循环遍历 Excel 文件和表](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)。  
  
## <a name="excel-connection-manager-editor"></a>Excel 连接管理器编辑器
  使用 **“Excel 连接管理器编辑器”** 对话框可以将连接添加到现有或新的 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 工作簿文件。  
  
 若要了解有关 Excel 连接管理器的详细信息，请参阅 [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md)。  
  
### <a name="options"></a>选项  
 **Excel 文件路径**  
 键入一个现有或新的 Excel 工作簿文件 (.xls) 的路径和文件名。  
  
> [!NOTE]  
>  无法连接到受密码保护的 Excel 文件。  
  
> [!WARNING]  
>  选择指向新的或不存在的文件的“Excel 连接”然后单击“Excel 工作表的名称”对应的“新建”时，“Excel 目标编辑器”将自动创建 Excel 文件。  
  
 **浏览**  
 使用“打开”对话框可以导航到 Excel 文件所在的文件夹或要创建新文件的文件夹。  
  
 **Excel 版本**  
 指定用于创建文件的 Microsoft Excel 的版本。  
  
 **首行包含列名称**  
 指定所选工作表中的第一行数据是否包含列名称。 此选项的默认值为 **True**。  
  
## <a name="connectivity-components-for-microsoft-excel-and-access-files"></a>Microsoft Excel 和 Access 文件的连接组件
  
可能需要下载 Microsoft Office 文件的连接组件（如果尚未安装）。 在此处下载用于 Excel 和 Access 文件的最新版连接组件：[Microsoft Access 数据库引擎 2016 可再发行组件](https://www.microsoft.com/download/details.aspx?id=54920)。
  
最新版组件可以打开 Excel 早期版本创建的文件。

如果计算机有 32 位版本的 Office，则必须安装 32 位版本的组件，还须确保在 32 位模式下运行程序包。

如果有 Office 365 订阅，请确保下载 Access 数据库引擎 2016 可再发行组件，而不是 Microsoft Access 2016 Runtime。 运行安装程序时，可能会看到一条错误消息，指出该下载项无法与 Office 即点即用组件并行安装。 若要绕过此错误消息，请打开命令提示符窗口并使用 `/quiet` 开关运行下载的 .EXE 文件，从而在安静模式下运行安装。 例如：

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`
  
## <a name="related-tasks"></a>相关任务  
  
-   [使用 Foreach 循环容器，循环遍历 Excel 文件和表](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
-   [连接到 Excel 工作簿](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)  
  
  
