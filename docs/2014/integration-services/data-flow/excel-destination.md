---
title: Excel 目标 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.exceldest.f1
helpviewer_keywords:
- destinations [Integration Services], Excel
- Excel [Integration Services]
ms.assetid: 37c07446-1264-4814-b4f5-9c66d333bb24
author: chugugrace
ms.author: chugu
ms.openlocfilehash: eff97cfad0091d2794d895f2f9b4ac086690bb05
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437824"
---
# <a name="excel-destination"></a>Excel 目标
  Excel 目标将数据加载到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 工作簿中的工作表或范围中。  
  
## <a name="access-modes"></a>访问模式  
 Excel 目标为数据加载提供了三种数据访问模式：  
  
-   表或视图。  
  
-   变量中指定的表或视图。  
  
-   SQL 语句的运行结果。 查询可以是参数化查询。  
  
> [!IMPORTANT]  
>  在 Excel 中，工作表或范围等同于表或视图。 Excel 源和目标编辑器中可用表的列表仅显示现有的工作表（以追加到电子表格名称之后的 $ 符号为标识，如 Sheet1$）和指定范围（以 $ 符号的缺失为标识，如 MyRange）。  
  
## <a name="usage-considerations"></a>使用注意事项  
 Excel 连接管理器使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Jet 4.0 及其支持的 Excel ISAM（索引顺序存取方法）驱动程序来连接 Excel 数据源，并在 Excel 数据源中进行数据读写操作。  
  
 许多现有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 知识库文章都记录了该访问接口和驱动程序的行为。虽然这些文章并非专门介绍 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 或其前身 Data Transformation Services，但您仍可了解到一些可能导致意外结果的行为。 有关 Excel 驱动程序的使用及行为的一般信息，请参阅 [如何将 ADO 与来自 Visual Basic 或 VBA 的 Excel 数据一起使用](https://support.microsoft.com/kb/257819)。  
  
 在将数据保存到 Excel 目标时，Excel 驱动程序所附带的 Jet 访问接口的以下行为可以导致意外的结果。  
  
-   **保存文本数据**。 Excel 驱动程序将文本数据值保存到 Excel 目标时，驱动程序将在每个单元内的文本之前添加单引号字符 (') 以确保所保存的值将被解释为文本值。 如果拥有或要开发将读取或处理所保存的数据的其他应用程序，则可能需要包括特殊的措施，以处理位于每个文本值前面的单引号字符。  
  
     有关如何避免包括单引号的信息，请参阅 msdn.com 上的博客文章： [在 SSIS 包中使用 Excel 目标数据流组件时，单引号会在数据转换成 Excel 时追加到所有字符串](https://go.microsoft.com/fwlink/?LinkId=400876)。  
  
-   **保存 memo (ntext) 数据**。 若要将大于 255 个字符的字符串成功地保存到 Excel 列中，驱动程序必须将该目标列的数据类型识别为 **memo** ，而不是 **string**。 如果目标表中已存在数据行，则由驱动程序抽样的前几行的 memo 列中必须至少包含一个长度大于 255 个字符的值的实例。 如果目标表是在包设计或运行时创建的，则 CREATE TABLE 语句必须使用 LONGTEXT （或其同义词之一）作为 memo 列的数据类型。  
  
-   **数据类型**。 Excel 驱动程序只识别有限的一组数据类型。 例如，所有数值列均解释为双精度 (DT_R8)，并且所有字符串列（除了 memo 列）均解释为 255 个字符的 Unicode 字符串 (DT_WSTR)。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 按如下所示方式映射 Excel 数据类型：  
  
    -   数值    双精度浮点 (DT_R8)  
  
    -   货币     货币 (DT_CY)  
  
    -   布尔     布尔 (DT_BOOL)  
  
    -   日期/时间 `datetime` （DT_DATE）  
  
    -   字符串     Unicode 字符串，长度为 255 (DT_WSTR)  
  
    -   Memo     Unicode 文本流 (DT_NTEXT)  
  
-   **数据类型和长度转换**。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 不隐式转换数据类型。 因此，在将 Excel 数据加载到非 Excel 目标中之前，可能需要使用“派生列”或“数据转换”转换机制显式地转换它，或者在将其加载到 Excel 目标中之前将其转换为非 Excel 数据。 这种情况下，可能需要通过使用导入和导出向导（它将自动配置所需转换）来创建初始包。 下面是一些可能必需的转换的示例：  
  
    -   Unicode Excel 字符串列与具有特定代码页的非 Unicode 字符串列之间的转换。  
  
    -   在 255 个字符的 Excel 字符串列和不同长度的字符串列之间转换。  
  
    -   双精度 Excel 数值列与其他类型的数值列之间的转换。  
  
## <a name="configuration-of-the-excel-destination"></a>Excel 目标的配置  
 Excel 目标使用 Excel 连接管理器连接到数据源，而连接管理器指定要使用的工作簿文件。 有关详细信息，请参阅 [Excel Connection Manager](../connection-manager/excel-connection-manager.md)。  
  
 Excel 目标具有一个常规输入和一个错误输出。  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 **“Excel 目标编辑器”** 对话框中设置的属性的详细信息，请单击下列主题之一：  
  
-   [Excel 目标编辑器（“连接管理器”页）](../excel-destination-editor-connection-manager-page.md)  
  
-   [Excel 目标编辑器（“映射”页）](../excel-destination-editor-mappings-page.md)  
  
-   [Excel 目标编辑器（“错误输出”页）](../excel-destination-editor-error-output-page.md)  
  
 **“高级编辑器”** 对话框反映了所有能以编程方式设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [通用属性](../common-properties.md)  
  
-   [Excel 自定义属性](excel-custom-properties.md)  
  
 有关如何设置属性的详细信息，请参阅 [设置数据流组件的属性](set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [使用 SQL Server Integration Services (SSIS) 将数据导入 Excel 或从 Excel 导出数据](../load-data-to-from-excel-with-ssis.md)  
  
-   [使用 Foreach 循环容器，循环遍历 Excel 文件和表](../control-flow/foreach-loop-container.md)  
  
-   [设置数据流组件的属性](set-the-properties-of-a-data-flow-component.md)  
  
## <a name="see-also"></a>另请参阅  
 [Excel 源](excel-source.md)   
 [Integration Services &#40;SSIS&#41; 变量](../integration-services-ssis-variables.md)   
 [数据流](data-flow.md)   
 [使用脚本任务处理 Excel 文件](../extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)  
  
  
