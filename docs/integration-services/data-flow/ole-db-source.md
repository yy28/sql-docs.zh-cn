---
title: OLE DB 源 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.oledbsource.f1
- sql13.dts.designer.oledbsourceadapter.connection.f1
- sql13.dts.designer.oledbsourceadapter.columns.f1
- sql13.dts.designer.oledbsourceadapter.errorhandling.f1
helpviewer_keywords:
- sources [Integration Services], OLE DB
- OLE DB source [Integration Services]
ms.assetid: f87cc5f6-b078-40f3-9d87-7a65e13e4c86
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b160f1a6aa71b612c80eb21daa8d2173376cee69
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2019
ms.locfileid: "58272980"
---
# <a name="ole-db-source"></a>OLE DB 源
  OLE DB 源通过使用数据库表、视图或 SQL 命令，从各种兼容 OLE DB 的关系数据库中提取数据。 例如，OLE DB 源可以从 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的表中提取数据。  
  
> [!NOTE]  
>  如果数据源是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007，则数据源需要一个不同于早期版本 Excel 的连接管理器。 有关详细信息，请参阅 [连接到 Excel 工作簿](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)。  
  
 OLE DB 源提供四种不同数据访问模式用于提取数据：  
  
-   表或视图。  
  
-   变量中指定的表或视图。  
  
-   SQL 语句的运行结果。 查询可以是参数化查询。  
  
-   存储在变量中的 SQL 语句的运行结果。  
  
> [!NOTE]  
>  在您使用 SQL 语句调用从临时表返回结果的某一存储过程时，使用 WITH RESULT SETS 选项可为结果集定义元数据。  
  
 如果使用参数化查询，则可以将变量映射到参数，以便在 SQL 语句中指定单个参数的值。  
  
 这个源使用 OLE DB 连接管理器连接到数据源，而该连接管理器则指定要使用的 OLE DB 访问接口。 有关详细信息，请参阅 [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md)。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 项目也提供可据以创建 OLE DB 连接管理器的数据源对象，从而使 OLE DB 源可以使用数据源和数据源视图。  
  
 根据不同的 OLE DB 访问接口，对 OLE DB 源存在一些限制：  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Oracle 不支持 Oracle 数据类型 BLOB、CLOB、NCLOB、BFILE 或 UROWID，因此，OLE DB 源不能从包含这些数据类型列的表中提取数据。  
  
-   IBM OLE DB DB2 访问接口和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB DB2 访问接口不支持使用调用存储过程的 SQL 命令。 如果使用这种命令，OLE DB 源将无法创建列元数据，这样一来，数据流中 OLE DB 源之后的数据流组件将没有可用的列数据，从而导致数据流执行失败。  
  
 OLE DB 源有一个常规输出和一个错误输出。  
  
## <a name="using-parameterized-sql-statements"></a>使用参数化 SQL 语句  
 OLE DB 源可以使用 SQL 语句来提取数据。 此语句可以是 SELECT 或 EXEC 语句。  
  
 OLE DB 源使用 OLE DB 连接管理器来连接到它从中提取数据的数据源。 取决于 OLE DB 连接管理器所使用的访问接口和连接管理器所连接的关系数据库管理系统 (RDBMS)，参数的命名和列出将应用不同的规则。 如果参数名是从 RDBMS 返回的，则可以使用参数名来将参数列表中的参数映射到 SQL 语句中的参数；否则，参数将按它们在参数列表中的序数位置映射到 SQL 语句中的参数。 支持的参数名类型按访问接口而各不相同。 例如，某些访问接口要求使用变量或列名称，而某些访问接口则要求使用诸如 0 或 Param0 这样的符号名称。 应当参阅访问接口对应的文档，了解有关在 SQL 语句中使用的参数名称的信息。  
  
 使用 OLE DB 连接管理器时，不能使用参数化子查询，这是因为 OLE DB 源不能通过 OLE DB 访问接口派生参数信息。 但是，可以使用表达式将参数值连接到查询字符串并设置该源的 SqlCommand 属性。在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中，可以使用“OLE DB 源编辑器”对话框配置 OLE DB 源，并在“设置查询参数”对话框中将参数映射到变量。  
  
### <a name="specifying-parameters-by-using-ordinal-positions"></a>使用序号位置指定参数  
 如果没有返回参数名，则 **“设置查询参数”** 对话框中的 **“参数”** 列表中的参数列出顺序将控制运行时参数将映射哪个参数标记。 列表中的第一个参数将映射到 SQL 语句中的第一个 ?， 第二个参数映射到第二个 ?，以此类推。  
  
 以下 SQL 语句选择 **数据库的** Product [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 表中的行。 **Mappings** 列表中的第一个参数映射到 **Color** 列的第一个参数，第二个参数映射到 **Size** 列。  
  
 `SELECT * FROM Production.Product WHERE Color = ? AND Size = ?`  
  
 参数名不受影响。 例如，如果参数与它所应用的列同名，但在 **“参数”** 列表中没有放在正确的序号位置，则在运行时发生的参数映射将使用参数的序号位置，而不是参数名称。  
  
 EXEC 命令通常要求在过程中使用提供参数值的变量的名称作为参数名称。  
  
### <a name="specifying-parameters-by-using-names"></a>使用名称来指定参数  
 如果实际参数名称是从 RDBMS 返回的，则 SELECT 和 EXEC 语句所使用的参数将按名称进行映射。 参数名称必须与存储过程（由 SELECT 语句或 EXEC 语句运行）所期望的名称匹配。  
  
 以下 SQL 语句运行 **uspGetWhereUsedProductID** 存储过程（在 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 数据库中可用）。  
  
 `EXEC uspGetWhereUsedProductID ?, ?`  
  
 存储过程希望变量 `@StartProductID` 和 `@CheckDate`提供参数值。 参数出现在 **“映射”** 列表中的顺序是不相关的。 唯一要求是，参数名必须与存储过程中的变量名一致，包括 \@ 符号在内。  
  
### <a name="mapping-parameters-to-variables"></a>将参数映射到变量  
 在运行时参数将映射到提供参数值的变量。 尽管也可以使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供的系统变量，但变量通常是用户定义变量。 如果使用用户定义变量，请确保将数据类型设置为与映射参数所引用的列的数据类型相兼容的类型。 有关详细信息，请参阅 [Integration Services (SSIS) 变量](../../integration-services/integration-services-ssis-variables.md)。  
  
## <a name="troubleshooting-the-ole-db-source"></a>OLE DB 源故障排除  
 可以记录 OLE DB 源对外部数据访问接口所做的调用。 利用此日志记录功能，可以对 OLE DB 源执行的从外部数据源加载数据的操作进行故障排除。 若要记录 OLE DB 源对外部数据访问接口所做的调用，请在包级别启用包日志记录并选择 **“诊断”** 事件。 有关详细信息，请参阅 [包执行的疑难解答工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
## <a name="configuring-the-ole-db-source"></a>配置 OLE DB 源  
 可以采用编程方式或通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器来设置属性。  
  
 **“高级编辑器”** 对话框反映了可以通过编程方式进行设置的属性。 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [OLE DB 自定义属性](../../integration-services/data-flow/ole-db-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [使用 OLE DB 源提取数据](../../integration-services/data-flow/extract-data-by-using-the-ole-db-source.md)  
  
-   [将查询参数映射到数据流组件中的变量](../../integration-services/data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
-   [设置数据流组件的属性](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [为合并转换和合并联接转换排序数据](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="related-content"></a>相关内容  
 social.technet.microsoft.com 上的 Wiki 文章 [SSIS 与 Oracle 连接器](https://go.microsoft.com/fwlink/?LinkId=220670)。  
  
## <a name="ole-db-source-editor-connection-manager-page"></a>OLE DB 源编辑器（“连接管理器”页）
  可以使用 **“OLE DB 源编辑器”** 对话框的 **“连接管理器”** 页，为源选择 OLE DB 连接管理器。 使用此页还可以选择数据库中的表或视图。  
  
> [!NOTE]  
>  若要从使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007 的数据源加载数据，请使用 OLE DB 源。 使用 Excel 源无法从 Excel 2007 数据源加载数据。 有关详细信息，请参阅 [Configure OLE DB Connection Manager](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)。  
>   
>  若要从使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2003 或更低版本的数据源加载数据，请使用 Excel 源。 有关详细信息，请参阅 [Excel 源编辑器（“连接管理器”页）](../../integration-services/data-flow/excel-source-editor-connection-manager-page.md)。  
  
> [!NOTE]  
>  OLE DB 源的 **CommandTimeout** 属性未在 **“OLE DB 源编辑器”** 中提供，但可以使用 **“高级编辑器”** 进行设置。 有关此属性的详细信息，请参阅 [OLE DB Custom Properties](../../integration-services/data-flow/ole-db-custom-properties.md)的“Excel 源”部分。  
  
### <a name="open-the-ole-db-source-editor-connection-manager-page"></a>打开“OLE DB 源编辑器”（“连接管理器”页）  
  
1.  在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中，向 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]包添加 OLE DB 源。  
  
2.  右键单击源组件，然后单击“编辑”。  
  
3.  单击 **“连接管理器”**。  
  
### <a name="static-options"></a>静态选项  
 **“无缓存”**  
 从列表中选择一个现有连接管理器，或通过单击“新建”创建一个新连接。  
  
 **新建**  
 通过使用“配置 OLE DB 连接管理器”对话框创建一个新连接管理器。  
  
 **数据访问模式**  
 指定从源选择数据的方法。  
  
|选项|描述|  
|------------|-----------------|  
|表或视图|从 OLE DB 数据源中的表或视图中检索数据。|  
|表名变量或视图名变量|在变量中指定表或视图名称。<br /><br /> **相关信息：**[在包中使用变量](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|SQL 命令|使用 SQL 查询从 OLE DB 数据源中检索数据。|  
|变量中的 SQL 命令|在变量中指定 SQL 查询文本。|  
  
 **预览**  
 通过使用“数据视图”对话框预览结果。 **预览版** 最多可以显示 200 行。  
  
> [!NOTE]  
>  预览数据时，数据类型为 CLR 用户定义类型的列不包含数据。 而是显示值“\<数值太大，无法显示>”或 System.Byte[]。 使用 SQL OLE DB 访问接口访问数据源时，显示前一个值；使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 访问接口访问数据源时，显示后一个值。  
  
### <a name="data-access-mode-dynamic-options"></a>数据访问模式动态选项  
  
#### <a name="data-access-mode--table-or-view"></a>数据访问模式 = 表或视图  
 **表或视图的名称**  
 从数据源的可用表列表或视图列表中选择表或视图的名称。  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>数据访问模式 = 表名变量或视图名变量  
 **变量名称**  
 选择包含表或视图名称的变量。  
  
#### <a name="data-access-mode--sql-command"></a>数据访问模式 = SQL 命令  
 **SQL 命令文本**  
 输入 SQL 查询的文本，通过单击“生成查询”来生成查询，或通过单击“浏览”定位到包含查询文本的文件。  
  
 **参数**  
 如果已经在参数化查询文本中使用 ? 作为参数占位符输入了参数化查询，请使用 **“设置查询参数”** 对话框将查询输入参数映射到包变量。  
  
 **生成查询**  
 使用“查询生成器”对话框可直观地构造 SQL 查询。  
  
 **“浏览”**  
 使用“打开”对话框可定位到包含 SQL 查询文本的文件。  
  
 **分析查询**  
 验证查询文本的语法。  
  
#### <a name="data-access-mode--sql-command-from-variable"></a>数据访问模式 = 变量中的 SQL 命令  
 **变量名称**  
 选择包含 SQL 查询文本的变量。  
  
## <a name="ole-db-source-editor-columns-page"></a>OLE DB 源编辑器（“列”页）
  可以使用“OLE DB 源编辑器”对话框的“列”页，将输出列映射到每个外部（源）列。  
  
### <a name="options"></a>选项  
 **可用外部列**  
 查看数据源中可用外部列的列表。 无法使用此表添加或删除列。  
  
 **“外部列”**  
 按照外部（源）列在您配置使用此源中数据的组件时的显示顺序，查看外部（源）列。 首先清除表中所选的列，然后以不同的顺序从列表中选择外部列，即可更改顺序。  
  
 **输出列**  
 为每个输出列提供唯一的名称。 默认值为所选外部（源）列的名称；不过，您也可以任选一个唯一的描述性名称。 所提供的名称将在 SSIS 设计器中显示。  
  
## <a name="ole-db-source-editor-error-output-page"></a>OLE DB 源编辑器（“错误输出”页）
  可以使用 **“OLE DB 源编辑器”** 对话框的 **“错误输出”** 页选择错误处理选项以及设置错误输出列的属性。  
  
### <a name="options"></a>选项  
 **输入/输出**  
 查看数据源的名称。  
  
 **列**  
 查看在“OLE DB 源编辑器”对话框中“连接管理器”页上选择的外部（源）列。  
  
 **错误**  
 指定发生错误时应执行的操作：忽略失败、重定向行或使组件失败。  
  
 **相关主题：**[数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **截断**  
 指定发生截断时应执行的操作：忽略失败、重定向行或使组件失败。  
  
 **Description**  
 查看对错误的说明。  
  
 **将此值设置到选定的单元格**  
 指定发生错误或截断时应对所有选定单元格执行的操作：忽略失败、重定向行或使组件失败。  
  
 **应用**  
 将错误处理选项应用到选定的单元格。  
  
## <a name="see-also"></a>另请参阅  
 [OLE DB 目标](../../integration-services/data-flow/ole-db-destination.md)   
 [Integration Services (SSIS) 变量](../../integration-services/integration-services-ssis-variables.md)   
 [数据流](../../integration-services/data-flow/data-flow.md)  
  
  
