---
title: "字词查找转换 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.termlookuptrans.f1
- sql13.dts.designer.termlookup.termlookup.f1
- sql13.dts.designer.termlookup.referencetable.f1
- sql13.dts.designer.termlookup.advanced.f1
helpviewer_keywords:
- extracting data [Integration Services]
- match extracted terms [Integration Services]
- text extraction [Integration Services]
- term extractions [Integration Services]
- lookups [Integration Services]
- counting extracted items
- Term Lookup transformation
ms.assetid: 3c0fa2f8-cb6a-4371-b184-7447be001de1
caps.latest.revision: 56
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 4b557efa62075f7b88e6b70cf5950546444b95d8
ms.openlocfilehash: ee1fa267107940169c05942e8614a7bf7148566a
ms.contentlocale: zh-cn
ms.lasthandoff: 08/19/2017

---
# <a name="term-lookup-transformation"></a>字词查找转换
  字词查找转换将从转换输入列的文本中提取的字词与引用表中的字词进行匹配， 然后计算出查找表中的字词在输入数据集中出现的次数，并将计数与引用表中的此字词一并写入转换输出的列中。 此转换对于创建基于输入文本并带有词频统计信息的自定义词列表很有用。  
  
 字词查找转换在执行查找之前，先使用与字词提取转换相同的方法从输入列的文本中提取词：  
  
-   将文本分割为句子。  
  
-   将句子分割为词。  
  
-   对词进行规范。  
  
 若要进一步自定义要匹配的字词，可以对字词查找转换进行配置，使其在查找匹配时区分大小写。  
  
## <a name="matches"></a>匹配  
 字词查找使用下列规则执行查找并返回值：  
  
-   如果转换被配置为在查找匹配项时区分大小写，那么它会放弃大小写不相符的匹配项。 例如， *student* 和 *STUDENT* 将视为不同的词。  
  
    > [!NOTE]  
    >  非大写字与位于句首的大写字可为匹配项。 例如，如果 *Student* 是句首词，则 *student* 和 *Student* 之间匹配成功。  
  
-   如果引用表中存在名词或名词短语的复数形式，则查找仅匹配该名词或名词短语的复数形式。 例如， *students* 的所有实例将与 *student*的实例分别计数。  
  
-   如果在引用表中只找到词的单数形式，则该词或短语的单数和复数形式都视为单数形式的匹配项。 例如，如果查找表包含 *student*，而转换找到两个词 *student* 和 *students*，则两个词都将计为查找字词 *student*的匹配项。  
  
-   如果输入列中的文本为还原的名词短语，则规范仅影响名词短语中的最后一个词。 例如， *doctors appointments* 的还原形式为 *doctors appointment*。  
  
 如果查找项包含的字词与引用集中的字词重叠，即一个子字词出现在多个引用记录中，则字词查找转换仅返回一个查找结果。 下面的示例显示查找项包含重叠子字词时的结果。 在本示例中，重叠的子字词为 *Windows*，它出现在两个引用字词中。 但是，转换并不返回两个结果，而仅返回一个引用字词 *Windows*。 第二个引用字词 *Windows 7 Professional*并未返回。  
  
|项|“值”|  
|----------|-----------|  
|输入字词|Windows 7 Professional|  
|引用字词|Windows、Windows 7 Professional|  
|输出|Windows|  
  
 字词查找转换可以匹配包含特殊字符的名词和名词短语，而引用表中的数据可能包含这些字符。 特殊字符如下所示: %，@，&、 $、 #、 \*，:，;，。， **，** ，！，？， \<，>，+，=，^，~，|， \\，/，（、）、 [、]、 {、}、"，和。  
  
## <a name="data-types"></a>数据类型  
 字词查找转换只能使用数据类型为 DT_WSTR 或 DT_NTEXT 的列。 如果列包含文本，但不具有这两种数据类型之一，则数据转换可以将数据类型为 DT_WSTR 或 DT_NTEXT 的列添加到数据流，并将列值复制到新列。 然后，数据转换的输出就可以用作字词查找转换的输入。 有关详细信息，请参阅 [Data Conversion Transformation](../../../integration-services/data-flow/transformations/data-conversion-transformation.md)。  
  
## <a name="configuration-the-term-lookup-transformation"></a>字词查找转换的配置  
 字词查找转换输入列包含 InputColumnType 属性，用于指示该列的用途。 InputColumnType 可能包含以下值：  
  
-   值 0 指示将列仅传递到输出，而不在查找中使用。  
  
-   值 1 指示仅在查找中使用列。  
  
-   值 2 指示将列传递到输出，并在查找中使用列。  
  
 InputColumnType 属性设置为 0 或 2 的转换输出列包含列的 CustomLineageID 属性，该属性包含由上游数据流组件分配给列的沿袭标识符。  
  
 字词查找转换还将两列添加到转换输出，默认名称分别为 **Term** 和 **Frequency**。 **Term** 包含查找表中的字词，而 **Frequency** 包含引用表中的字词在输入数据集中出现的次数。 这些列不包含 CustomLineageID 属性。  
  
 查找表必须是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 或 Access 数据库中的表。 如果将字词提取转换的输出保存到表，则可以使用此表作为引用表，但也可以使用其他表。 必须先将平面文件中、Excel 工作簿或其他源的文本导入到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库或 Access 数据库，然后才能使用字词查找转换。  
  
 字词查找转换使用单独的 OLE DB 连接来连接到引用表。 有关详细信息，请参阅 [OLE DB Connection Manager](../../../integration-services/connection-manager/ole-db-connection-manager.md)。  
  
 字词查找转换以完全预缓存模式工作。 运行时，字词查找转换先从引用表中读取字词并将其存储到自己的专用内存，然后再处理转换输入行。  
  
 因为输入列行中的字词可能重复，所以字词查找转换的输出通常具有比转换输入更多的行。  
  
 此转换具有一个输入和一个输出。 它不支持错误输出。  
  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [通用属性](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [转换自定义属性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 有关如何设置属性的详细信息，请参阅 [设置数据流组件的属性](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="term-lookup-transformation-editor-term-lookup-tab"></a>字词查找转换编辑器（“字词查找”选项卡）
  可以使用 **“字词查找转换编辑器”** 对话框的 **“字词查找”** 选项卡，将输入列映射到引用表中的查找列，以及为每个输出列提供别名。  
  
### <a name="options"></a>选项  
 **可用输入列**  
 使用复选框选择要传递给未更改输出的输入列。 将输入列拖动到 **“可用引用列”** 列表可以将其映射到引用表中的查找列。 输入列和查找列必须具有支持的匹配数据类型（DT_NTEXT 或 DT_WSTR）。 选择一个映射行，再右键单击可在 [创建关系](../../../integration-services/data-flow/transformations/create-relationships.md) 对话框中编辑该映射。  
  
 **“可用引用列”**  
 查看引用表中可用的列。 选择包含要匹配的字词列表的列。  
  
 **传递列**  
 从可用输入列的列表中进行选择。 通过选中 **“可用输入列”** 表中的复选框来选择列。  
  
 **输出列别名**  
 为每个输出列键入一个别名。 默认值为列的名称；不过，您也可以任选一个唯一的描述性名称。  
  
 **配置错误输出**  
 使用 [配置错误输出](http://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) 对话框可以为导致错误的行指定错误处理方式选项。  
  
## <a name="term-lookup-transformation-editor-reference-table-tab"></a>字词查找转换编辑器（“引用表”选项卡）
  可以使用“字词查找转换编辑器”对话框的“引用表”选项卡指定到引用（查找）表的连接。  
  
### <a name="options"></a>选项  
 **“无缓存”**  
 从列表中选择一个现有连接管理器，或通过单击“新建”创建一个新连接。  
  
 **新建**  
 通过使用“配置 OLE DB 连接管理器”对话框创建新的连接。  
  
 **引用表的名称**  
 通过从该列表中选择项，可以从数据库中选择查找表或视图。 查找表或视图应包含具有现有字词列表的列，以便源列中的文本可以与这些字词进行比较。  
  
 **配置错误输出**  
 使用 [配置错误输出](http://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) 对话框可以为导致错误的行指定错误处理方式选项。  
  
## <a name="term-lookup-transformation-editor-advanced-tab"></a>字词查找转换编辑器（“高级”选项卡）
  可以使用“字词查找转换编辑器”对话框的“高级”选项卡指定查找是否区分大小写。  
  
### <a name="options"></a>选项  
 **使用区分大小写的字词查找**  
 指示查找是否区分大小写。 默认值为 **False**。  
  
 **配置错误输出**  
 使用 [配置错误输出](http://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) 对话框可以为导致错误的行指定错误处理方式选项。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../../integration-services/integration-services-error-and-message-reference.md)   
 [字词提取转换](../../../integration-services/data-flow/transformations/term-extraction-transformation.md)  
  

