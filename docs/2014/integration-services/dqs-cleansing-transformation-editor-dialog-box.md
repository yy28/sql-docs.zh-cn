---
title: DQS 清除转换编辑器对话框 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssdqs.designer.cleansing.f1
- SQL12.SSDQS.DESIGNER.DQCONNECTION.F1
ms.assetid: 07e79641-71ee-45d0-a9ba-ed6f9f68f333
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c6367e846f3b542101db5c4328cd99e1a16f0416
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62898865"
---
# <a name="dqs-cleansing-transformation-editor-dialog-box"></a>“DQS 清除转换编辑器”对话框
  可使用 Data Quality Services (DQS) 通过“DQS 清除转换编辑器”对话框来更正数据。 有关详细信息，请参阅 [Data Quality Services Concepts](../../2014/data-quality-services/data-quality-services-concepts.md)。  
  
 若要了解有关转换的详细信息，请参阅 [DQS Cleansing Transformation](data-flow/transformations/dqs-cleansing-transformation.md)。  
  
 **您希望做什么？**  
  
-   [打开 DQS 清除转换编辑器](#open)  
  
-   [设置“连接管理器”选项卡上的选项](#connection)  
  
-   [设置“映射”选项卡上的选项](#mapping)  
  
-   [设置“高级”选项卡上的选项](#advanced)  
  
-   [设置“DQS 清除连接管理器”对话框中的选项](#manager)  
  
##  <a name="open"></a> 打开 DQS 清除转换编辑器  
  
1.  在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中，将“DQS 清除转换”添加到 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]包。  
  
2.  右键单击该组件，然后单击 **“编辑”**。  
  
##  <a name="connection"></a> 设置“连接管理器”选项卡上的选项  
 **数据质量连接管理器**  
 从列表中选择现有 DQS 连接管理器，或单击“新建”创建一个新连接。  
  
 **新建**  
 使用“DQS 清除连接管理器”对话框创建新的连接管理器。 请参阅 [设置“DQS 清除连接管理器”对话框中的选项](#manager)  
  
 **数据质量知识库**  
 为所连接的数据源选择现有的 DQS 知识库。 有关 DQS 知识库的详细信息，请参阅 [DQS Knowledge Bases and Domains](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md)。  
  
 **加密连接**  
 指定是否加密连接，以便对 DQS 服务器之间的数据传输进行加密和[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]。  
  
 **可用域**  
 列出可用于选定知识库的域。 存在两种类型的域：单一域和包含两个或两个以上的单一域的复合域。  
  
 有关如何将列映射到复合域的信息，请参阅 [Map Columns to Composite Domains](data-flow/transformations/map-columns-to-composite-domains.md)。  
  
 有关域的详细信息，请参阅 [DQS Knowledge Bases and Domains](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md)。  
  
 **配置错误输出**  
 指定如何处理行级错误。 在转换更正来自已连接数据源的数据时可能会由于意外的数据值或验证约束而出错。  
  
 有效值如下：  
  
-   **“组件失败”**，指示转换失败并且输入数据未插入 Data Quality Services 数据库中。 这是默认值。  
  
-   **“重定向行”**，指示输入数据未插入 Data Quality Services 数据库中并且重定向到错误输出。  
  
##  <a name="mapping"></a> 设置“映射”选项卡上的选项  
 有关如何将列映射到复合域的信息，请参阅 [Map Columns to Composite Domains](data-flow/transformations/map-columns-to-composite-domains.md)。  
  
 **可用输入列**  
 列出所连接数据源中的列。 选择包含要更正的数据的一个或多个列。  
  
 **输入列**  
 列出你在“可用输入列”区域中选定的输入列。  
  
 **域**  
 选择要映射到输入列的域。  
  
 **源别名**  
 列出包含原始列值的源列。  
  
 在该字段中单击可修改列名。  
  
 **输出别名**  
 列出“DQS 清除转换”输出的列。 该列包含原始列值或更正的值。  
  
 在该字段中单击可修改列名。  
  
 **状态别名**  
 列出包含已更正数据的状态信息的列。 在该字段中单击可修改列名。  
  
##  <a name="advanced"></a> 设置“高级”选项卡上的选项  
 **标准化输出**  
 指示是否根据为域定义的输出格式以标准化格式输出数据。 有关标准化格式的详细信息，请参阅 [数据清理](../../2014/data-quality-services/data-cleansing.md)。  
  
 **置信度**  
 指示是否包括已更正数据的置信度。 置信度指示 DQS 对更正或建议的确信程度。 有关置信度的详细信息，请参阅 [数据清理](../../2014/data-quality-services/data-cleansing.md)。  
  
 **原因**  
 指示是否包括数据更正的原因。  
  
 **追加的数据**  
 指示是否输出从现有的引用数据访问接口接收的附加数据。 有关详细信息，请参阅 [Reference Data Services in DQS](../../2014/data-quality-services/reference-data-services-in-dqs.md)。  
  
 **追加的数据架构**  
 指示是否输出数据架构。 有关详细信息，请参阅[将域或复合域附加到引用数据](../../2014/data-quality-services/attach-a-domain-or-composite-domain-to-reference-data.md)。  
  
##  <a name="manager"></a> 设置“DQS 清除连接管理器”对话框中的选项  
 **服务器名称**  
 选择或键入要连接的 DQS 服务器的名称。 有关该服务器的详细信息，请参阅 [DQS Administration](../../2014/data-quality-services/dqs-administration.md)。  
  
 **测试连接**  
 单击该选项可以确认您指定的连接是否有效。  
  
 您还可以通过执行以下操作从连接区域打开 **“DQS 清除连接管理器”** 对话框：  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开现有的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目或者创建一个新项目。  
  
2.  在连接区域中单击右键，依次单击“新建连接”和“DQS”。  
  
3.  单击 **“添加”**。  
  
## <a name="see-also"></a>请参阅  
 [将数据质量规则应用于数据源](data-flow/transformations/apply-data-quality-rules-to-data-source.md)  
  
  
