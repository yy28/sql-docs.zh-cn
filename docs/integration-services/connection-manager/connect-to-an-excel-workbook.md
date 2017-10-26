---
title: "连接到 Excel 工作簿 |Microsoft 文档"
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Excel [Integration Services]
ms.assetid: d9746318-3669-4ce2-bbb0-4a1bd471c9dd
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2800075091835b2d6f2b07ee34e9b897fe86634e
ms.openlocfilehash: f8fb1db80ac1b750950a3401516b54af5ee29686
ms.contentlocale: zh-cn
ms.lasthandoff: 08/17/2017

---
# <a name="connect-to-an-excel-workbook"></a>连接到 Excel 工作簿
  若要将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包连接到 Microsoft Office Excel 工作簿，需要 Excel 连接管理器。  
  
 您可以从 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器的“连接管理器”区域或从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导，创建这些连接管理器。  
 
## <a name="connectivity-components-for-microsoft-excel-and-access-files"></a>Microsoft Excel 和 Access 文件的连接组件
  
你可能需要下载 Microsoft Office 文件的连接组件，如果它们尚未安装。 下载最新版本的 Excel 和 Access 文件此处连接组件： [Microsoft Access 数据库引擎 2016年可再发行组件](https://www.microsoft.com/download/details.aspx?id=54920)。
  
组件的最新版本可以打开的 Excel 的早期版本创建的文件。

如果计算机具有 32 位版本的 Office，那么您需要安装 32 位版本的组件，并还需要确保在 32 位模式下运行包。

如果你有 Office 365 订阅，请确保你下载访问数据库引擎 2016年可再发行组件和不是 Microsoft 访问 2016年运行时。 运行安装程序时，可能会看到一条错误消息，您无法下载通过并行安装 Office 单击以运行组件。 要跳过此错误消息，并已成功安装组件，运行安装程序在静默模式下打开命令提示符窗口并运行。使用下载的 EXE 文件`/quiet`切换。 例如：

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="create-an-excel-connection-manager"></a>创建 Excel 连接管理器

### <a name="to-create-an-excel-connection-manager-from-the-connection-managers-area"></a>从“连接管理器”区域创建 Excel 连接管理器  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开该包。  
  
2.  在“连接管理器”区域中，右键单击该区域中的任意位置，然后选择“新建连接”。  
  
3.  在 **“添加 SSIS 连接管理器”** 对话框中，选择 **Excel**，然后配置该连接管理器。  
  
     有关适用于此连接管理器的配置选项的信息，请参阅 [Excel Connection Manager Editor](../../integration-services/connection-manager/excel-connection-manager-editor.md)。  
  
### <a name="to-create-an-excel-connection-from-the-sql-server-import-and-export-wizard"></a>从 SQL Server 导入和导出向导创建 Excel 连接  
  
1.  启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导的 32 位版本。  
  
2.  在 **“选择数据源”** 页上，选择 **Microsoft Excel**作为 **“数据源”**，然后配置该 Excel 连接。  
  
     有关适用于此连接类型的配置选项的信息，请参阅 [Excel Connection Manager Editor](../../integration-services/connection-manager/excel-connection-manager-editor.md)。  
  
## <a name="see-also"></a>另请参阅  
 [连接到 Access 数据库](../../integration-services/connection-manager/connect-to-an-access-database.md)  
  
  

