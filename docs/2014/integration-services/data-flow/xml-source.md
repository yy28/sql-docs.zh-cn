---
title: XML 源 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.xmlsource.f1
helpviewer_keywords:
- sources [Integration Services], XML
- XML source [Integration Services]
- XML Source Editor
ms.assetid: 68c27ea5-e93d-4e26-bfb2-d967ca0a5282
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 0cd1817bbf9b3cdca4181e8fb32dfbe76fd59dc7
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939198"
---
# <a name="xml-source"></a>XML 源
  XML 源读取 XML 数据文件，并用数据填充源输出中的列。  
  
 XML 文件中的数据常常包含层次结构关系。 例如，XML 数据文件可以表示目录和目录中的项。 必须先确定 XML 数据文件中元素的关系，并且为文件中的每个元素都生成了一个输出，数据才能进入数据流。  
  
## <a name="schemas"></a>架构  
 XML 源使用某种架构来解释 XML 数据。 XML 源支持使用 XML 架构定义 (XSD) 文件或内联架构将 XML 数据解释为表格格式。 如果使用 **“XML 源编辑器”** 对话框配置 XML 源，用户界面可以根据指定的 XML 数据文件生成 XSD。  
  
> [!NOTE]  
>  不支持 DTD。  
  
 这些架构仅可以支持一个命名空间；不支持架构集合。  
  
> [!NOTE]  
>  XML 源并不根据 XSD 来验证 XML 文件中的数据。  
  
## <a name="xml-source-editor"></a>XML 源编辑器  
 XML 文件中的数据常常包含层次结构关系。 **“XML 源编辑器”** 对话框使用指定的架构生成 XML 源输出。 您可以指定 XSD 文件，使用内联架构或根据指定的 XML 数据文件生成 XSD。 该架构必须在设计时可用。  
  
 XML 源通过为 XML 文件中每个包含其他元素的元素创建一个输出，以便根据 XML 数据生成表格结构。 例如，如果 XML 数据表示目录和目录中的项，则 XML 源将为目录创建一个输出，而且为目录包含的每种类型的项都创建一个输出。 每项的输出将包含该项的属性的输出列。  
  
 为了在输出中提供关于数据层次结构关系的信息，XML 源在输出中添加了一个为各个子元素标识父元素的列。 通过使用带有不同类型项的目录示例，每个项将具有一个用于标识该项所属目录的列值。  
  
 XML 源为每个元素创建一个输出，但您不需要使用所有输出。 您可以删除不想使用的输出，或只是不将其连接到下游组件。  
  
 XMl 源还生成输出名称，以确保输出名称明确。 这些名称可能比较长，而且可能没有以对您有用的方式标识输出。 可以重命名输出，但是要保持其名称的唯一性。 还可以修改输出列的数据类型和长度。  
  
 对于每个输出，XML 源都会添加一个错误输出。 默认情况下，错误输出中的列的数据类型为 Unicode 字符串数据类型 (DT_WSTR)，列的长度为 255 个字符，但您可以通过修改列的数据类型和长度来配置错误输出中的列。  
  
 如果 XML 数据文件包含 XSD 中没有的元素，则这些元素将被忽略，并且不会为其生成输出。 另一方面，如果 XML 数据文件缺少 XSD 中存在的元素，则输出将包含空值列。  
  
 从 XML 数据文件提取数据后，数据将转换为 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型。 不过，XML 源不能将 XML 数据转换为 DT_TIME2 或 DT_DBTIMESTAMP2 数据类型，这是因为源不支持这些数据类型。 有关详细信息，请参阅 [Integration Services 数据类型](integration-services-data-types.md)。  
  
 XSD 或内联架构可能为元素指定了数据类型，但如果未指定，则“XML 源编辑器”  对话框将为输出中包含该元素的列指定 Unicode 字符串数据类型 (DT_WSTR)，并将列长度设置为 255 个字符。  
  
 如果该架构指定了元素的最大长度，则输出列的长度将设置为此值。 如果最大长度大于将元素转换为的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型所支持的长度，则数据将被截断为该数据类型的最大长度。 例如，如果一个字符串的长度为 5000，则该字符串将因为 DT_WSTR 数据类型的最大长度而截断为 4000 字符；类似地，字节数据将截断为 DT_BYTES 数据类型的最大长度 8000 字符。 如果架构未指定最大长度，则具有任何一种数据类型的列的默认长度都设置为 255。 对 XML 源中的数据截断的处理方式与其他数据流组件中截断的处理方式相同。 有关详细信息，请参阅 [数据中的错误处理](error-handling-in-data.md)。  
  
 您可以修改数据类型和列长度。 有关详细信息，请参阅 [Integration Services 数据类型](integration-services-data-types.md)。  
  
## <a name="configuration-of-the-xml-source"></a>XML 源的配置  
 XML 源支持三种不同的数据访问模式。 您可以指定 XML 数据文件的文件位置、包含文件位置的变量或包含 XML 数据的变量。  
  
 XML 源包括可以在加载包时通过属性表达式进行更新的 `XMLData` 和 `XMLSchemaDefinition` 自定义属性。 有关详细信息，请参阅 [Integration Services (SSIS) 表达式](../expressions/integration-services-ssis-expressions.md)、[在包中使用属性表达式](../expressions/use-property-expressions-in-packages.md)和 [XML 源自定义属性](xml-source-custom-properties.md)。  
  
 XML 源支持多个常规输出和多个错误输出。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含用于配置 XML 源的“XML 源编辑器”对话框  。 此对话框在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中可用。  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 **“XML 源编辑器”** 对话框中设置的属性的详细信息，请单击下列主题之一：  
  
-   [XML 源编辑器（“连接管理器”页）](../xml-source-editor-connection-manager-page.md)  
  
-   [XML 源编辑器（“列”页）](../xml-source-editor-columns-page.md)  
  
-   [XML 源编辑器（“错误输出”页）](../xml-source-editor-error-output-page.md)  
  
 **“高级编辑器”** 对话框反映了可以通过编程方式进行设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [通用属性](../common-properties.md)  
  
-   [XML 源自定义属性](xml-source-custom-properties.md)  
  
 有关如何设置属性的详细信息，请单击下列主题之一：  
  
-   [设置数据流组件的属性](set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [使用 XML 源提取数据](xml-source.md)  
  
## <a name="related-content"></a>相关内容  
 技术文章，[使用 XML 文件配置 SSIS 包](https://www.sqlshack.com/using-xml-file-configure-ssis-package/)。  
  
  
