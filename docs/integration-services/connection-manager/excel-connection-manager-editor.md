---
title: "Excel 连接管理器编辑器 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.excelconnection.f1"
helpviewer_keywords: 
  - "Excel 连接管理器编辑器"
ms.assetid: 7ff097e4-cafb-4885-a898-05b2a46628c1
caps.latest.revision: 32
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 32
---
# Excel 连接管理器编辑器
  使用 **“Excel 连接管理器编辑器”** 对话框可以将连接添加到现有或新的 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 工作簿文件。  
  
 若要了解有关 Excel 连接管理器的详细信息，请参阅 [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md)。  
  
## 选项  
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
  
## Microsoft Excel 和 Access 文件的提供程序和驱动程序  
 你可能需要下载 Microsoft Office 文件的的 OLE DB 提供程序和驱动程序（如果它们尚未安装）。 更高版本的提供程序可以打开 Excel 的早期版本所创建的文件。  
  
 如果计算机有 32 位版本的 Office，则必须安装 32 位版本的驱动程序，并且你还必须确保运行向导或它在 32 位模式下创建的 Integration Services 包。  
  
|Microsoft Office 版本|下载|  
|------------------------------|--------------|  
|2007|[2007 Office System Driver: Data Connectivity Components（Office 2007 系统驱动程序：数据连接组件）](https://www.microsoft.com/download/details.aspx?id=23734)|  
|2010|[Microsoft Access 2010 Runtime](https://www.microsoft.com/download/details.aspx?id=10910)|  
|2013|[Microsoft Access 2013 Runtime](http://www.microsoft.com/download/details.aspx?id=39358)|  
|2016|[Microsoft Access 2016 Runtime](https://www.microsoft.com/download/details.aspx?id=50040)|
  
## 另请参阅  
 [Integration Services 错误和消息引用](../../integration-services/integration-services-error-and-message-reference.md)   
 [使用 Foreach 循环容器循环遍历 Excel 文件和表](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
  