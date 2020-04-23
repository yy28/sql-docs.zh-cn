---
title: Excel 源 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.excelsource.f1
helpviewer_keywords:
- Excel [Integration Services]
- sources [Integration Services], Excel
ms.assetid: e66349f3-b1b8-4763-89b7-7803541a4d62
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 37eb17ccaa418a6d81ef4caa461af50e505a8747
ms.sourcegitcommit: c37777216fb8b464e33cd6e2ffbedb6860971b0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "82087147"
---
# <a name="excel-source"></a>Excel 源
  Excel 源从 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 工作簿的工作表或范围中提取数据。  
  
 Excel 源提供了四种提取数据的数据访问方式：  
  
-   表或视图。  
  
-   变量中指定的表或视图。  
  
-   SQL 语句的运行结果。 查询可以是参数化查询。  
  
-   存储在变量中的 SQL 语句的运行结果。  
  
> [!IMPORTANT]  
>  在 Excel 中，工作表或范围等同于表或视图。 Excel 源和目标编辑器中的可用表列表显示现有工作表（以追加到工作表名称后的 $ 符号标识，如 Sheet1$）和命名区域（不用 $ 符号标识，如 MyRange）。 有关详细信息，请参阅“使用注意事项”部分。  
  
 Excel 源使用 Excel 连接管理器与数据源建立连接，连接管理器可指定要使用的工作簿文件。 有关详细信息，请参阅 [Excel Connection Manager](../connection-manager/excel-connection-manager.md)。  
  
 Excel 源有一个常规输出和一个错误输出。  
  
## <a name="usage-considerations"></a>使用注意事项  
 Excel 连接管理器使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Jet 4.0 及其支持的 Excel ISAM（索引顺序存取方法）驱动程序来连接 Excel 数据源，并在 Excel 数据源中进行数据读写操作。  
  
 许多现有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 知识库文章都记录了该访问接口和驱动程序的行为。虽然这些文章并非专门介绍 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 或其前身 Data Transformation Services，但您仍可了解到一些可能导致意外结果的行为。 有关 Excel 驱动程序的使用及行为的一般信息，请参阅 [如何将 ADO 与来自 Visual Basic 或 VBA 的 Excel 数据一起使用](https://support.microsoft.com/kb/257819)。  
  
 当从 Excel 数据源读取数据时，Jet 访问接口和 Excel 驱动程序的下列行为可能会导致意外结果。  
  
-   **数据源**. Excel 工作簿中的数据源可以是工作表（必须追加 $ 符号，如 Sheet1$）或命名区域（如 MyRange）。 在 SQL 语句中，工作表的名称必须加以分隔（如 [Sheet1$]），以避免 $ 符号引起语法错误。 查询生成器可自动添加这些分隔符。 指定工作表或范围时，该驱动程序将读取从工作表或范围左上角第一个非空单元开始的连续单元块。 因此，源数据中不能有空行，在标题或页眉行与数据行之间也不能有空行。  
  
-   **缺少值**。 Excel 驱动程序读取指定源中一定数量的行（默认情况下为 8 行）以推测每列的数据类型。 如果推测出列可能包含混合数据类型（尤其是混合了文本数据的数值数据时），驱动程序将决定采用占多数的数据类型，并对包含其他类型数据的单元返回 Null 值。 （如果各种数据类型的数量相当，则采用数值类型。）Excel 工作表中大部分单元格格式设置选项不会影响此数据类型判断。 可以通过指定导入模式来修改 Excel 驱动程序的此行为。 要指定导入模式，请在`IMEX=1`**"属性"** 窗口中的 Excel 连接管理器的连接字符串中添加"扩展属性"的值。 有关详细信息，请参阅 [PRB: Excel Values Returned as NULL Using DAO OpenRecordset（PRB：使用 DAO OpenRecordset 返回的 Excel NULL 值）](https://support.microsoft.com/kb/194124)。  
  
-   **截断的文本**。 驱动程序在确定 Excel 列是否包含文本数据时，它将基于采样的最长值来选择数据类型（字符串或 memo）。 如果驱动程序没有在其采样的行中发现任何长于 255 个字符的值，那么它会将该列视为 255 个字符的字符串的列而不是 memo 列。 因此，长度超过 255 个字符的值可能会被截断。 若要从 memo 列导入数据而不发生截断，必须确保至少一个采样行中的 memo 列包含的值的长度超过 255 个字符，否则必须增加驱动程序采样的行数，使其包括这样的行。 你可以通过增加 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Jet\4.0\Engines\Excel** 注册表项下的 **TypeGuessRows** 的值来增加用作示例的行数。 有关详细信息，请参阅 [PRB：从 Jet 4.0 OLEDB 源传输数据失败并出现错误](https://support.microsoft.com/kb/281517)。  
  
-   **数据类型**。 Excel 驱动程序只识别有限的一组数据类型。 例如，所有数值列均解释为双精度 (DT_R8)，并且所有字符串列（除了 memo 列）均解释为 255 个字符的 Unicode 字符串 (DT_WSTR)。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 按如下所示方式映射 Excel 数据类型：  
  
    -   数值 - 双精度浮点 (DT_R8)  
  
    -   货币 - 货币 (DT_CY)  
  
    -   布尔 - 布尔 (DT_BOOL)  
  
    -   日期/时间`datetime`- （DT_DATE）  
  
    -   字符串 - Unicode 字符串，长度为 255 (DT_WSTR)  
  
    -   Memo - Unicode 文本流 (DT_NTEXT)  
  
-   **数据类型和长度转换**。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 不隐式转换数据类型。 因此，在将其加载到非 Excel 目标之前，可能需要使用“派生列”或“数据转换”转换来显式转换 Excel 数据，或在将它加载到 Excel 目标之前，对非 Excel 数据进行转换。 这种情况下，可能需要通过使用导入和导出向导（它将自动配置所需转换）来创建初始包。 下面是一些可能必需的转换的示例：  
  
    -   Unicode Excel 字符串列与具有特定代码页的非 Unicode 字符串列之间的转换  
  
    -   在 255 个字符的 Excel 字符串列和不同长度的字符串列之间转换  
  
    -   双精度 Excel 数值列与其他类型的数值列之间的转换  
  
## <a name="excel-source-configuration"></a>Excel 源配置  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 **“Excel 源编辑器”** 对话框中设置的属性的详细信息，请单击下列主题之一：  
  
-   [Excel 源编辑器（“连接管理器”页）](../excel-source-editor-connection-manager-page.md)  
  
-   [Excel 源编辑器（“列”页）](../excel-source-editor-columns-page.md)  
  
-   [Excel 源编辑器（“错误输出”页）](../excel-source-editor-error-output-page.md)  
  
 **“高级编辑器”** 对话框反映了所有能以编程方式设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [通用属性](../common-properties.md)  
  
-   [Excel 自定义属性](excel-custom-properties.md)  
  
 有关循环遍历 Excel 文件中的某个组的信息，请参阅 [使用 Foreach 循环容器，循环遍历 Excel 文件和表](../control-flow/foreach-loop-container.md)。  
  
## <a name="related-tasks"></a>Related Tasks  

-   [使用 SQL Server Integration Services (SSIS) 将数据导入 Excel 或从 Excel 导出数据](../load-data-to-from-excel-with-ssis.md)

-   [将查询参数映射到数据流组件中的变量](map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
-   [设置数据流组件的属性](set-the-properties-of-a-data-flow-component.md)  
  
-   [为合并转换和合并联接转换排序数据](transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
-   [使用 Foreach 循环容器，循环遍历 Excel 文件和表](../control-flow/foreach-loop-container.md)  
  
## <a name="related-content"></a>相关内容  
  
-   hrvoje.piasevoli.com 上的博客文章： [在 SSIS 中从 64 位 Excel 导入数据](https://go.microsoft.com/fwlink/?LinkId=217673)。  
  
-   博客条目，[连接到 SSIS 中的 Excel （XLSX）。](https://microsoft-ssis.blogspot.com/2014/02/connecting-to-excel-xlsx-in-ssis.html)  
  
  
