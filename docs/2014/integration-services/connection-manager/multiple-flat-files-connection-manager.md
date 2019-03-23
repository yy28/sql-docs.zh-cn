---
title: 多平面文件连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Multiple Flat Files connection manager
- connections [Integration Services], flat files
- flat files
- flat file connections [Integration Services]
- connection managers [Integration Services], Multiple Flat Files
- multiple flat file connections
ms.assetid: 31fc3f7a-d323-44f5-a907-1fa3de66631a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7235f5f333ac7bb4520a6244e103baafba343ea3
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58391935"
---
# <a name="multiple-flat-files-connection-manager"></a>多平面文件连接管理器
  多平面文件连接管理器使包可以访问多个平面文件中的数据。 例如，数据流任务在循环容器（例如 For 循环容器）内时，平面文件源可以使用多平面文件连接管理器。 在容器的每个循环中，平面文件源从多平面文件连接管理器提供的下一个文件名加载数据。  
  
 在将多个平面文件连接管理器添加到包中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]创建连接将解析为在运行时，集多平面文件连接管理器，属性的多个平面文件连接管理器和将多个平面文件连接管理器为`Connections`包的集合。  
  
 该连接管理器的 `ConnectionManagerType` 属性设置为 `MULTIFLATFILE`。  
  
 可以按下列方式配置多平面文件连接管理器：  
  
-   指定要使用的文件、区域设置和代码页。 区域设置用于解释受区域设置影响的数据（如日期），代码页用于将字符串数据转换为 Unicode。  
  
-   指定文件格式。 可以使用带分隔符、具有固定宽度或右边未对齐的文件格式。  
  
-   指定标题行、数据流和列分隔符。 列分隔符可以在文件级别设置，而在列级别被覆盖。  
  
-   指示文件中的第一行是否包含列名称。  
  
-   指定文本限定符。 可以将每一列配置为识别文本限定符。  
  
-   对各列设置诸如名称、数据类型和最大宽度等属性。  
  
 当多平面文件连接管理器引用多个文件时，文件的路径由竖线 (|) 分隔。 连接管理器的 `ConnectionString` 属性的格式如下：  
  
 \<路径>|\<路径>  
  
 也可以使用通配符来指定多个文件。 例如，为驱动器 C 上的所有文本文件的值的引用`ConnectionString`属性可以设置为 c:\\*.txt。  
  
 如果多平面文件连接管理器引用多个文件，则所有文件必须具有相同格式。  
  
 默认情况下，多平面文件连接管理器将字符串列的长度设置为 50 个字符。 在 **“多个平面文件连接管理器编辑器”** 对话框中，可以计算示例数据，并自动调整这些列的长度大小，以防止发生数据截断或超过列宽的情况。 除非在平面文件源或转换过程中调整列长度的大小，否则列长度将在整个数据流中保持不变。 如果这些列映射到更窄的目标列，则用户界面将显示警告，在运行时，则可能由于数据截断而发生错误。 可以在平面文件连接管理器、平面文件源或转换过程中调整列的大小，以便与目标列兼容。 若要修改输出列的长度，则设置`Length`上的输出列的属性**输入和输出属性**选项卡中**高级编辑器**对话框。  
  
 在已添加并配置了使用连接管理器的平面文件源之后，如果在多平面文件连接管理器中更新了列长度，则不必在平面文件源中手动调整输出列的大小。 打开 **“平面文件源”** 对话框时，平面文件源将提供同步列元数据的选项。  
  
## <a name="configuration-of-the-multiple-flat-files-connection-manager"></a>多平面文件连接管理器的配置  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击下列主题之一：  
  
-   [多平面文件连接管理器编辑器（“常规”页）](../general-page-of-integration-services-designers-options.md)  
  
-   [多平面文件连接管理器编辑器（“列”页）](../multiple-flat-files-connection-manager-editor-columns-page.md)  
  
-   [多平面文件连接管理器编辑器（“高级”页）](../multiple-flat-files-connection-manager-editor-advanced-page.md)  
  
-   [多平面文件连接管理器编辑器（“预览”页）](../multiple-flat-files-connection-manager-editor-preview-page.md)  
  
 有关以编程方式配置连接管理器的信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以编程方式添加连接](../building-packages-programmatically/adding-connections-programmatically.md)项目。  
  
## <a name="see-also"></a>请参阅  
 [“平面文件源”](../data-flow/flat-file-source.md)   
 [平面文件目标](../data-flow/flat-file-destination.md)   
 [Integration Services (SSIS) 连接](integration-services-ssis-connections.md)  
  
  
