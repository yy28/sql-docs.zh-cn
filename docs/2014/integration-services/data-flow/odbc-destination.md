---
title: ODBC 目标 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcdest.f1
ms.assetid: bffa63e0-c737-4b54-b4ea-495a400ffcf8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e398766c827f7611432f5ecd94353f1168e136b4
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85431894"
---
# <a name="odbc-destination"></a>ODBC 目标
  ODBC 目标可以将数据大容量加载到支持 ODBC 的数据库表中。 ODBC 目标使用 ODBC DB 连接管理器来连接到数据源。  
  
 ODBC 目标包括输入列和目标数据源中的列之间的映射。 您不必将输入列映射到所有目标列，但有时如果没有将输入列映射到目标列可能会出错，具体取决于目标列的属性。 例如，如果目标列不允许出现 Null 值，则必须将输入列映射到该列。 此外，可以映射不同类型的列，但是，如果输入数据与目标列类型不兼容，则在运行时会出现错误。 根据错误行为设置，将忽略该错误，并且导致失败，或者行将发送到错误输出。  
  
 ODBC 目标具有一个常规输出和一个错误输出。  
  
##  <a name="load-options"></a><a name="BKMK_odbcdestination_loadoptions"></a> 加载选项  
 ODBC 目标可以使用两个访问加载模块之一。 在 [ODBC 源编辑器（“连接管理器”页）](../odbc-source-editor-connection-manager-page.md)中设置模式。 这两种模式是：  
  
-   **批处理**：在此模式中，ODBC 目标将基于发现的 ODBC 访问接口功能尝试使用最高效的插入方法。 对于大多数现今的 ODBC 访问接口，这意味着准备具有参数的 INSERT 语句，然后使用按行数组参数绑定（其中，数组大小由 **BatchSize** 属性控制）。 如果选择“批处理”  并且提供程序不支持此方法，则 ODBC 目标将自动切换到“逐行”  模式。  
  
-   **逐行**：在此模式中，ODBC 目标准备具有参数的 INSERT 语句并且使用“SQL 执行”  来一次一行地插入行。  
  
## <a name="error-handling"></a>错误处理  
 ODBC 目标有一个错误输出。 组件的错误输出包括以下输出列：  
  
-   **错误代码**：与当前错误相对应的编号。 有关错误的列表，请参阅源数据库的文档。 有关 SSIS 错误代码的列表，请参阅 SSIS 错误代码和消息参考。  
  
-   **错误列**：导致错误（针对转换错误）的源列。  
  
-   标准的输出数据列。  
  
 根据错误行为设置，CDC 目标支持在错误输出中返回在提取过程中发生的错误（数据转换、截断）。 有关详细信息，请参阅 [ODBC 源编辑器（“错误输出”页）](../odbc-source-editor-error-output-page.md)。  
  
## <a name="parallelism"></a>并行度  
 对于可对同一台计算机或不同计算机（并非一般的全局会话限制）上的相同表或不同表并行运行的 ODBC 目标组件的数目没有限制。  
  
 但是，要使用的 ODBC 访问接口的限制可能会限制通过该访问接口的同时连接的数目。 这些限制将会限制 ODBC 目标可能支持的并行实例的数目。 SSIS 开发人员必须知道要使用的任何 ODBC 访问接口的限制并且在生成 SSIS 包时将这些限制元素考虑进去。  
  
 您还必须知道，同时加载到同一个表中可能会由于标准记录锁定而降低性能。 这取决于要加载的数据和表的组织结构。  
  
## <a name="troubleshooting-the-odbc-destination"></a>ODBC 目标故障排除  
 可以记录 ODBC 源对外部数据访问接口所做的调用。 利用此日志记录功能，可以排除 ODBC 目标执行将数据保存到外部数据源的操作过程中发生的故障。 若要记录 ODBC 目标对外部数据访问接口进行的调用，请启用 ODBC 驱动程序管理器跟踪。 有关详细信息，请参阅 Microsoft 文档 *数据源管理员如何使用 ODBC 生成 ODBC 跟踪*。  
  
## <a name="configuring-the-odbc-destination"></a>配置 ODBC 目标  
 您可以通过编程方式或者通过 SSIS 设计器配置 ODBC 目标。  
  
 有关详细信息，请参阅下列主题之一：  
  
-   [ODBC 目标编辑器（“连接管理器”页）](../odbc-destination-editor-connection-manager-page.md)  
  
-   [ODBC 目标编辑器（“映射”页）](../odbc-destination-editor-mappings-page.md)  
  
-   [ODBC 目标编辑器（“错误输出”页）](../odbc-destination-editor-error-output-page.md)  
  
 **“高级编辑器”** 对话框包含可通过编程方式设置的属性。  
  
 打开 **“高级编辑器”** 对话框：  
  
-   在您的 **项目的** “数据流” [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 屏幕上，右键单击 ODBC 目标，然后选择 **“显示高级编辑器”** 。  
  
 有关可在“高级编辑器”对话框中设置的属性的详细信息，请参阅 [ODBC Destination Custom Properties](odbc-destination-custom-properties.md)。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [ODBC 目标编辑器（“错误输出”页）](../odbc-destination-editor-error-output-page.md)  
  
-   [ODBC 目标编辑器（“映射”页）](../odbc-destination-editor-mappings-page.md)  
  
-   [ODBC 目标编辑器（“连接管理器”页）](../odbc-destination-editor-connection-manager-page.md)  
  
-   [通过使用 ODBC 目标来加载数据](odbc-destination.md)  
  
-   [ODBC Destination Custom Properties](odbc-destination-custom-properties.md)  
  
  
