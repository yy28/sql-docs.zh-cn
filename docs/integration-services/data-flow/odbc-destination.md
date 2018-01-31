---
title: "ODBC 目标 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
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
- sql13.ssis.designer.odbcdest.f1
- sql13.ssis.designer.odbcdest.connection.f1
- sql13.ssis.designer.odbcdest.columns.f1
- sql13.ssis.designer.odbcdest.errorhandling.f1
ms.assetid: bffa63e0-c737-4b54-b4ea-495a400ffcf8
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 34e524470a56b62657f231a22639fc3e2c20e2d1
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="odbc-destination"></a>ODBC 目标
  ODBC 目标可以将数据大容量加载到支持 ODBC 的数据库表中。 ODBC 目标使用 ODBC DB 连接管理器来连接到数据源。  
  
 ODBC 目标包括输入列和目标数据源中的列之间的映射。 您不必将输入列映射到所有目标列，但有时如果没有将输入列映射到目标列可能会出错，具体取决于目标列的属性。 例如，如果目标列不允许出现 Null 值，则必须将输入列映射到该列。 此外，可以映射不同类型的列，但是，如果输入数据与目标列类型不兼容，则在运行时会出现错误。 根据错误行为设置，将忽略该错误，并且导致失败，或者行将发送到错误输出。  
  
 ODBC 目标具有一个常规输出和一个错误输出。  
  
##  <a name="BKMK_odbcdestination_loadoptions"></a> 加载选项  
 ODBC 目标可以使用两个访问加载模块之一。 在 [ODBC 源编辑器（“连接管理器”页）](../../integration-services/data-flow/odbc-source-editor-connection-manager-page.md)中设置模式。 这两种模式是：  
  
-   **批处理**：在此模式中，ODBC 目标将基于发现的 ODBC 访问接口功能尝试使用最高效的插入方法。 对于大多数现今的 ODBC 访问接口，这意味着准备具有参数的 INSERT 语句，然后使用按行数组参数绑定（其中，数组大小由 **BatchSize** 属性控制）。 如果选择“批处理”并且提供程序不支持此方法，则 ODBC 目标将自动切换到“逐行”模式。  
  
-   **逐行**：在此模式中，ODBC 目标准备具有参数的 INSERT 语句并且使用“SQL 执行”来一次一行地插入行。  
  
## <a name="error-handling"></a>错误处理  
 ODBC 目标有一个错误输出。 组件的错误输出包括以下输出列：  
  
-   **错误代码**：与当前错误相对应的编号。 有关错误的列表，请参阅源数据库的文档。 有关 SSIS 错误代码的列表，请参阅 SSIS 错误代码和消息参考。  
  
-   **错误列**：导致错误（针对转换错误）的源列。  
  
-   标准的输出数据列。  
  
 根据错误行为设置，CDC 目标支持在错误输出中返回在提取过程中发生的错误（数据转换、截断）。 有关详细信息，请参阅 [ODBC 源编辑器（“错误输出”页）](../../integration-services/data-flow/odbc-source-editor-error-output-page.md)。  
  
## <a name="parallelism"></a>并行  
 对于可对同一台计算机或不同计算机（并非一般的全局会话限制）上的相同表或不同表并行运行的 ODBC 目标组件的数目没有限制。  
  
 但是，要使用的 ODBC 访问接口的限制可能会限制通过该访问接口的同时连接的数目。 这些限制将会限制 ODBC 目标可能支持的并行实例的数目。 SSIS 开发人员必须知道要使用的任何 ODBC 访问接口的限制并且在生成 SSIS 包时将这些限制元素考虑进去。  
  
 您还必须知道，同时加载到同一个表中可能会由于标准记录锁定而降低性能。 这取决于要加载的数据和表的组织结构。  
  
## <a name="troubleshooting-the-odbc-destination"></a>ODBC 目标故障排除  
 可以记录 ODBC 源对外部数据访问接口所做的调用。 利用此日志记录功能，可以排除 ODBC 目标执行将数据保存到外部数据源的操作过程中发生的故障。 若要记录 ODBC 目标对外部数据访问接口进行的调用，请启用 ODBC 驱动程序管理器跟踪。 有关详细信息，请参阅 Microsoft 文档 *数据源管理员如何使用 ODBC 生成 ODBC 跟踪*。  
  
## <a name="configuring-the-odbc-destination"></a>配置 ODBC 目标  
 您可以通过编程方式或者通过 SSIS 设计器配置 ODBC 目标。  
  
 有关详细信息，请参阅下列主题之一：  
  
-   [ODBC 目标编辑器（“连接管理器”页）](../../integration-services/data-flow/odbc-destination-editor-connection-manager-page.md)  
  
-   [ODBC 目标编辑器（“映射”页）](../../integration-services/data-flow/odbc-destination-editor-mappings-page.md)  
  
-   [ODBC 目标编辑器（“错误输出”页）](../../integration-services/data-flow/odbc-destination-editor-error-output-page.md)  
  
 **“高级编辑器”** 对话框包含可通过编程方式设置的属性。  
  
 打开 **“高级编辑器”** 对话框：  
  
-   在您的 **项目的** “数据流” [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 屏幕上，右键单击 ODBC 目标，然后选择 **“显示高级编辑器”**。  
  
 有关可在“高级编辑器”对话框中设置的属性的详细信息，请参阅 [ODBC Destination Custom Properties](../../integration-services/data-flow/odbc-destination-custom-properties.md)。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [通过使用 ODBC 目标来加载数据](../../integration-services/data-flow/load-data-by-using-the-odbc-destination.md)  
  
-   [ODBC 目标自定义属性](../../integration-services/data-flow/odbc-destination-custom-properties.md)  
  
## <a name="odbc-destination-editor-connection-manager-page"></a>ODBC 目标编辑器（“连接管理器”页）
  可以使用 **“ODBC 目标编辑器”** 对话框的 **“连接管理器”** 页，为目标选择 ODBC 连接管理器。 使用此页还可以选择数据库中的表或视图。  
  
 **打开“ODBC 目标编辑器”的“连接管理器”页**  
  
### <a name="task-list"></a>任务列表  
  
-   在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，打开包含 ODBC 目标的 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 包。  
  
-   在“数据流”选项卡上，双击 ODBC 目标。  
  
-   在 **“ODBC 目标编辑器”**中，单击 **“连接管理器”**。  
  
### <a name="options"></a>“常规”  
  
#### <a name="connection-manager"></a>“ODBC 源编辑器”  
 从列表中选择现有 ODBC 连接管理器，或单击“新建”创建新的连接。 该连接可以指向支持 ODBC 的任何数据库。  
  
#### <a name="new"></a>新版  
 单击 **“新建”**。 **“配置 ODBC 连接管理器编辑器”** 对话框随即打开，供您在其中创建新的连接管理器。  
  
#### <a name="data-access-mode"></a>数据访问模式  
 选择将数据加载到目标的方法。 选项显示在下表中：  
  
|选项|Description|  
|------------|-----------------|  
|表名 - 批处理|选择此选项可将 ODBC 目标配置为在批处理模式下工作。 选择此选项后，以下选项可用：|  
||**表或视图的名称**：从列表中选择可用的表或视图。<br /><br /> 该列表仅包含前 1000 个表。 如果你的数据库包含超过 1000 个表，则可以键入表名的开头，或者使用 (\*) 通配符输入名称的任何部分以便显示要使用的表。<br /><br /> **批大小**：键入用于大容量加载的批处理的大小。 这是作为一批加载的行数。|  
|表名 - 逐行|选择此选项可以将 ODBC 目标配置为一次一行将各行插入目标表中。 选择此选项后，以下选项可用：|  
||**表或视图的名称**：从列表中选择数据库中的可用表或视图。<br /><br /> 该列表仅包含前 1000 个表。 如果您的数据库包含超过 1000 个表，则可以键入表名的开头，或者使用 (*) 通配符输入名称的任何部分以便显示要使用的表。|  
  
#### <a name="preview"></a>预览  
 单击 **“预览”** 可以查看所选表的最多 200 行数据。  
  
## <a name="odbc-destination-editor-mappings-page"></a>ODBC 目标编辑器（“映射”页）
  可以使用 **“ODBC 目标编辑器”** 对话框的 **“映射”** 页，将输入列映射到目标列。  
  
### <a name="options"></a>“常规”  
  
#### <a name="available-input-columns"></a>可用输入列  
 可用输入列的列表。 将输入列拖放到某一可用目标列以映射这些列。  
  
#### <a name="available-destination-columns"></a>可用目标列  
 可用目标列的列表。 将目标列拖放到某一可用输入列以映射这些列。  
  
#### <a name="input-column"></a>输入列  
 查看选定的输入列。 可以通过选择“\<忽略>”以从输出中排除列来移除映射。  
  
#### <a name="destination-column"></a>目标列  
 查看所有可用目标列（包括映射和未映射的列）。  
  
## <a name="odbc-destination-editor-error-output-page"></a>ODBC 目标编辑器（“错误输出”页）
  可以使用 **“ODBC 目标编辑器”** 对话框的 **“错误输出”** 页选择错误处理选项。  
  
 **打开 ODBC 目标编辑器的“错误输出”页**  
  
### <a name="task-list"></a>任务列表  
  
-   在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，打开包含 ODBC 目标的 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 包。  
  
-   在“数据流”选项卡上，双击 ODBC 目标。  
  
-   在 **“ODBC 目标编辑器”**中，单击 **“错误输出”**。  
  
### <a name="options"></a>“常规”  
  
#### <a name="inputoutput"></a>输入/输出  
 查看数据源的名称。  
  
#### <a name="column"></a>“列”  
 未使用。  
  
#### <a name="error"></a>错误  
 选择 ODBC 目标应该如何处理流中的错误：忽略失败、重定向行或使组件失败。  
  
#### <a name="truncation"></a>截断  
 选择 ODBC 目标应该如何处理流中的截断：忽略失败、重定向行或使组件失败。  
  
#### <a name="description"></a>Description  
 查看错误说明。  
  
#### <a name="set-this-value-to-selected-cells"></a>将此值设置到选定的单元格  
 选择发生错误或截断时 ODBC 目标应如何处理所有选定的单元格：忽略失败、重定向行或使组件失败。  
  
#### <a name="apply"></a>应用  
 将错误处理选项应用到选定的单元格。  
  
### <a name="error-handling-options"></a>错误处理选项  
 使用下列选项来配置 ODBC 目标处理错误和截断的方式。  
  
#### <a name="fail-component"></a>组件失败  
 发生错误或截断时数据流任务失败。 这是默认行为。  
  
#### <a name="ignore-failure"></a>忽略失败  
 忽略错误或截断。  
  
#### <a name="redirect-flow"></a>重定向流  
 将引起错误或截断的行定向到 ODBC 目标的错误输出。 有关详细信息，请参阅 ODBC 目标。  
  
