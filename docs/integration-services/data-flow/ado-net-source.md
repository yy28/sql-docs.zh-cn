---
title: ADO NET 源 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.adonetsource.f1
- sql13.dts.designer.adonetsource.connection.f1
- sql13.dts.designer.adonetsource.columns.f1
- sql13.dts.designer.adonetsource.erroroutput.f1
helpviewer_keywords:
- ADO.NET source
- sources [Integration Services], ADO.NET
- sources [Integration Services], DataReader
- .NET Framework [Integration Services]
- DataReader source
ms.assetid: 2a2f1750-2cda-4dda-9dca-623a96a6b3c0
caps.latest.revision: 101
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4142fa0f9a01631574cca90a3a21b2047cd30820
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="ado-net-source"></a>ADO NET 源
  ADO NET 源使用来自 .NET 提供程序的数据，并使这些数据对数据流可用。  
  
 你可以使用 ADO NET 源连接到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]。 不支持使用 OLE DB 连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 。 有关 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]的详细信息，请参阅 [通用指导原则和限制（Microsoft Azure SQL 数据库）](http://go.microsoft.com/fwlink/?LinkId=248228)。  
  
## <a name="data-type-support"></a>数据类型支持  
 源会将未映射到特定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型的任意数据类型转换为 DT_NTEXT [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型。 即使数据类型为 **System.Object**，也会发生此转换。  
  
 可以将 DT_NTEXT 数据类型更改为 DT_WSTR 数据类型，也可以将 DT_WSTR 更改为 DT_NTEXT。 通过在 ADO NET 源的 **“高级编辑器”** 对话框中设置 **DataType** 属性可更改数据类型。 有关详细信息，请参阅 [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)。  
  
 通过在 ADO NET 源之后使用数据转换，还可以将 DT_NTEXT 数据类型转换为 DT_BYTES 或 DT_STR 数据类型。 有关详细信息，请参阅 [Data Conversion Transformation](../../integration-services/data-flow/transformations/data-conversion-transformation.md)。  
  
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]中，日期数据类型 DT_DBDATE、DT_DBTIME2、DT_DBTIMESTAMP2 和 DT_DBTIMESTAMPOFFSET 映射到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的某些日期数据类型。 您可以配置 ADO NET 源，从而将日期数据类型从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用的数据类型转换为 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 使用的数据类型。 若要配置 ADO NET 源以便转换这些日期数据类型，请将 **连接管理器的** Type System Version [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 属性设置为 **Latest**。 （**Type System Version** 属性位于“连接管理器”对话框的“全部”页。 若要打开“连接管理器”对话框，请右键单击 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器，然后单击“编辑”。  
  
> [!NOTE]  
>  如果将 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器的 **Type System Version** 属性设置为**SQL Server 2005**，则系统会将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 日期数据类型转换为 DT_WSTR。  
  
 当 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 连接管理器将提供程序指定为 .NET Data Provider for [!INCLUDE[vstecado](../../includes/vstecado-md.md)] (SqlClient) 时，系统会将用户定义的数据类型 (UDT) 转换为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 二进制大型对象 (BLOB)。 当系统转换 UDT 数据类型时会应用下列规则：  
  
-   如果数据是非大型 UDT，系统会将该数据转换为 DT_BYTES。  
  
-   如果数据是非大型 UDT，并且数据库中列的 **Length** 属性设置为 -1 或大于 8,000 个字节的值，则系统会将该数据转换为 DT_IMAGE。  
  
-   如果数据是大型 UDT，系统会将该数据转换为 DT_IMAGE。  
  
    > [!NOTE]  
    >  如果 ADO NET 源未配置为使用错误输出，则系统会以 8,000 个字节为单位成块地使数据流向 DT_IMAGE 列。 如果 ADO NET 源配置为使用错误输出，则系统会将整个字节数组传递到 DT_IMAGE 列。 有关如何将组件配置为使用错误输出的详细信息，请参阅 [数据中的错误处理](../../integration-services/data-flow/error-handling-in-data.md)。  
  
 有关 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型、支持的数据类型转换以及某些数据库（包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]）之间的数据类型映射的详细信息，请参阅 [Integration Services 数据类型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
 有关将 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 数据类型映射为托管数据类型的详细信息，请参阅 [在数据流中使用数据类型](../../integration-services/extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md)。  
  
## <a name="ado-net-source-troubleshooting"></a>ADO NET 源故障排除  
 可以记录 ADO NET 源对外部数据访问接口所做的调用。 利用此日志记录功能，可以对 ADO NET 源执行的从外部数据源加载数据的操作进行故障排除。 若要记录 ADO NET 源对外部数据访问接口所做的调用，请在包级别启用包日志记录并选择 **“诊断”** 事件。 有关详细信息，请参阅 [包执行的疑难解答工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
## <a name="ado-net-source-configuration"></a>ADO NET 源配置  
 通过提供定义结果集的 SQL 语句可以配置 ADO NET 源。 例如，连接到 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 数据库并使用 SQL 语句 `SELECT * FROM Production.Product` 的 ADO NET 源可从 **Production.Product** 表提取所有行，并将数据集提供给下游组件。  
  
> [!NOTE]  
>  在您使用 SQL 语句调用从临时表返回结果的某一存储过程时，使用 WITH RESULT SETS 选项可为结果集定义元数据。  
  
> [!NOTE]  
>  如果使用 SQL 语句来执行存储过程且包因为以下错误失败，则可以通过在 exec 语句前添加 **SET FMTONLY OFF** 语句来更正错误。  
>   
>  **在数据源中找不到列 <列名>。**  
  
 ADO NET 源使用 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器连接到数据源，该连接管理器指定 .NET 提供程序。 有关详细信息，请参阅 [ADO.NET Connection Manager](../../integration-services/connection-manager/ado-net-connection-manager.md)。  
  
 ADO NET 源有一个常规输出和一个错误输出。  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式设置属性。  
  
 有关可以在 **“高级编辑器”** 对话框中或以编程方式设置的属性的详细信息，请单击下列主题之一：  
  
-   [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [ADO NET 自定义属性](../../integration-services/data-flow/ado-net-custom-properties.md)  
  
 有关如何设置属性的详细信息，请参阅 [设置数据流组件的属性](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)。  
  
## <a name="ado-net-source-editor-connection-manager-page"></a>ADO NET 源编辑器（“连接管理器”页）
  可以使用 **“ADO NET 源编辑器”** 对话框的 **“连接管理器”** 页，为源选择 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 连接管理器。 使用此页还可以选择数据库中的表或视图。  
  
 若要了解有关 ADO NET 源的详细信息，请参阅 [ADO NET Source](../../integration-services/data-flow/ado-net-source.md)。  
  
 **打开“连接管理器”页**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开具有 ADO NET 源的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。  
  
2.  在“数据流”选项卡上，双击 ADO NET 源。  
  
3.  在 **“ADO NET 源编辑器”**中，单击 **“连接管理器”**。  
  
### <a name="static-options"></a>静态选项  
 **ADO.NET 连接管理器**  
 从列表中选择一个现有连接管理器，或通过单击“新建”创建一个新连接。  
  
 **新建**  
 使用“配置 ADO.NET 连接管理器”对话框创建新的连接管理器。  
  
 **数据访问模式**  
 指定从源选择数据的方法。  
  
|选项|Description|  
|------------|-----------------|  
|表或视图|从 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 数据源中的表或视图中检索数据。|  
|SQL 命令|使用 SQL 查询从 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 数据源中检索数据。|  
  
 **预览**  
 通过使用“数据视图”对话框预览结果。 **预览版** 最多可以显示 200 行。  
  
> [!NOTE]  
>  预览数据时，数据类型为 CLR 用户定义类型的列不包含数据。 而是显示值“\<数值太大，无法显示>”或 System.Byte[]。 使用 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 访问接口访问数据源时，显示前一个值；使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 访问接口访问数据源时，显示后一个值。  
  
### <a name="data-access-mode-dynamic-options"></a>数据访问模式动态选项  
  
#### <a name="data-access-mode--table-or-view"></a>数据访问模式 = 表或视图  
 **表或视图的名称**  
 从数据源的可用表列表或视图列表中选择表或视图的名称。  
  
#### <a name="data-access-mode--sql-command"></a>数据访问模式 = SQL 命令  
 **SQL 命令文本**  
 输入 SQL 查询的文本，通过单击“生成查询”来生成查询，或通过单击“浏览”定位到包含查询文本的文件。  
  
 **生成查询**  
 使用“查询生成器”对话框可直观地构造 SQL 查询。  
  
 **“浏览”**  
 使用“打开”对话框可定位到包含 SQL 查询文本的文件。  
  
## <a name="ado-net-source-editor-columns-page"></a>ADO NET 源编辑器（“列”页）
  可以使用“ADO NET 源编辑器”对话框的“列”页，将输出列映射到每个外部（源）列。  
  
 若要了解有关 ADO NET 源的详细信息，请参阅 [ADO NET Source](../../integration-services/data-flow/ado-net-source.md)。  
  
 **打开“列”页**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开具有 ADO NET 源的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。  
  
2.  在“数据流”选项卡上，双击 ADO NET 源。  
  
3.  在 **“ADO NET 源编辑器”**中，单击 **“列”**。  
  
### <a name="options"></a>“常规”  
 **可用外部列**  
 查看数据源中可用外部列的列表。 无法使用此表添加或删除列。  
  
 **“外部列”**  
 按照外部（源）列在您配置使用此源中数据的组件时的显示顺序，查看外部（源）列。  
  
 **输出列**  
 为每个输出列提供唯一的名称。 默认值为所选外部（源）列的名称；不过，您也可以任选一个唯一的描述性名称。 所提供的名称将显示在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中。  
  
## <a name="ado-net-source-editor-error-output-page"></a>ADO NET 源编辑器（“错误输出”页）
  可以使用 **“ADO NET 源编辑器”** 对话框的 **“错误输出”** 页，选择错误处理选项以及设置错误输出列的属性。  
  
 若要了解有关 ADO NET 源的详细信息，请参阅 [ADO NET Source](../../integration-services/data-flow/ado-net-source.md)。  
  
 **打开“错误输出”页**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开具有 ADO NET 源的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包。  
  
2.  在“数据流”选项卡上，双击 ADO NET 源。  
  
3.  在 **“ADO NET 源编辑器”**中，单击 **“错误输出”**。  
  
### <a name="options"></a>“常规”  
 **输入/输出**  
 查看数据源的名称。  
  
 **列**  
 查看在“ADO NET 源编辑器”对话框的“连接管理器”页上选择的外部（源）列。  
  
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
 [DataReader 目标](../../integration-services/data-flow/datareader-destination.md)   
 [ADO NET 目标](../../integration-services/data-flow/ado-net-destination.md)   
 [数据流](../../integration-services/data-flow/data-flow.md)  
  
  
