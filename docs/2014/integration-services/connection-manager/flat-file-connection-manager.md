---
title: 平面文件连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connection managers [Integration Services], Flat File
- connections [Integration Services], flat files
- files [Integration Services], connections
- Flat File connection manager
- flat files
- flat file connections [Integration Services]
ms.assetid: 7830f80d-af32-4e8f-a6fc-f03af6bc1946
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4466ebd24647520c7cbba2bf0baa93a0f60a72bf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62833806"
---
# <a name="flat-file-connection-manager"></a>平面文件连接管理器
  平面文件连接管理器使包可以访问平面文件中的数据。 例如，平面文件源和目标可以使用平面文件连接管理器提取和加载数据。  
  
 平面文件连接管理器只能访问一个文件。 若要引用多个文件，请使用多平面文件连接管理器，而不用平面文件连接管理器。 有关详细信息，请参阅 [Multiple Flat Files Connection Manager](multiple-flat-files-connection-manager.md)。  
  
## <a name="column-length"></a>列长度  
 默认情况下，平面文件连接管理器会将字符串列的长度设置为 50 个字符。 在 **“平面文件连接管理器编辑器”** 对话框中，可以计算示例数据，并自动调整这些列的长度，以防止发生数据截断或超过列宽的情况。 而且，除非随后在平面文件源或转换中调整列长度，否则字符串列的列长度将在整个数据流中保持不变。 如果这些字符串列映射到更窄的目标列，用户界面中将显示警告。 此外，在运行时，可能由于数据截断而发生错误。 若要避免错误或截断，可以在平面文件连接管理器、平面文件源或转换中调整列的大小，以便与目标列兼容。 若要修改输出列的长度，则设置`Length`上的输出列的属性**输入和输出属性**选项卡中**高级编辑器**对话框。  
  
 在已添加并配置使用连接管理器的平面文件源之后，如果在平面文件连接管理器中更新列长度，则不必在平面文件源中手动调整输出列的大小。 打开 **“平面文件源”** 对话框时，平面文件源将提供同步列元数据的选项。  
  
## <a name="configuration-of-the-flat-file-connection-manager"></a>平面文件连接管理器的配置  
 在将平面文件连接管理器添加到包中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]创建的连接管理器将解析为平面文件连接在运行时，设置平面文件连接属性，并将添加到的平面文件连接管理器`Connections`包的集合。  
  
 该连接管理器的 `ConnectionManagerType` 属性设置为 `FLATFILE`。  
  
 默认情况下，平面文件连接管理器始终检查未被引号引起的数据中的行分隔符，在找到行分隔符时开始一个新行。 这使连接管理器可以正确地分析具有缺少列字段的行的文件。  
  
 在某些情况下，禁用此功能可以提高包性能。 可以通过设置平面文件连接管理器属性禁用此功能**AlwaysCheckForRowDelimiters**到`False`。  
  
 可以按下列方式配置平面文件连接管理器：  
  
-   指定要使用的文件、区域设置和代码页。 区域设置用于解释受区域设置影响的数据（如日期），代码页用于将字符串数据转换为 Unicode。  
  
-   指定文件格式。 可以使用带分隔符、具有固定宽度或右边未对齐的文件格式。  
  
-   指定标题行、数据流和列分隔符。 列分隔符可以在文件级别设置，而在列级别被覆盖。  
  
-   指示文件中的第一行是否包含列名称。  
  
-   指定文本限定符。 可以将每一列配置为识别文本限定符。  
  
     现在支持将限定符嵌入限定的字符串。 文本限定符的双实例将被解释为文字，即该字符串的单个实例。 例如，如果文本限定符是单引号并且输入数据为 'abc'、'def'、'g'hi'，则输出数据为 abc、def、g'hi。  
  
-   对各列设置诸如名称、数据类型和最大宽度等属性。  
  
 通过在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的“属性”窗口中指定表达式，可以设置平面文件连接管理器的 ConnectionString 属性。 为避免验证错误，请执行以下操作。  
  
-   使用表达式指定文件时，在 **“平面文件连接管理器编辑器”** 的 **“文件名”** 框中添加文件路径。  
  
-   将平面文件连接管理器的 **“DelayValidation”** 属性设置为 **“True”**。  
  
 使用平面文件连接管理器和平面文件目标，您可以在运行时使用表达式创建文件名。  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击下列主题之一：  
  
-   [平面文件连接管理器编辑器（“常规”页）](../general-page-of-integration-services-designers-options.md)  
  
-   [平面文件连接管理器编辑器（“列”页）](../flat-file-connection-manager-editor-columns-page.md)  
  
-   [平面文件连接管理器编辑器（“高级”页）](../flat-file-connection-manager-editor-advanced-page.md)  
  
-   [平面文件连接管理器编辑器（“预览”页）](../flat-file-connection-manager-editor-preview-page.md)  
  
 有关以编程方式配置连接管理器的信息，请参阅 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以编程方式添加连接](../building-packages-programmatically/adding-connections-programmatically.md)项目。  
  
  
