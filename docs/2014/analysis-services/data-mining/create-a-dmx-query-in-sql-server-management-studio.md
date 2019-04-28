---
title: SQL Server Management Studio 中创建 DMX 查询 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- templates [Analysis Services], queries
- SQL Server Management Studio [Analysis Services], DMX queries
- predictions [Analysis Services], DMX prediction queries
- predictions [DMX]
- prediction queries [DMX]
- queries [DMX], prediction queries
- mining models [Analysis Services], DMX
ms.assetid: 568ce40a-1f53-47eb-8c79-14347cdfde83
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c68e181a1ad0992e85c638accad26a0418be4b5e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62715344"
---
# <a name="create-a-dmx-query-in-sql-server-management-studio"></a>在 SQL Server Management Studio 中创建一个 DMX 查询
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了一组功能，可帮助您创建针对挖掘模型和挖掘结构的预测查询、内容查询和数据定义查询。  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中都提供了图形预测查询生成器，旨在简化编写预测查询并将数据集映射到模型的过程。  
  
-   模板资源管理器中提供的查询模板可快速创建多种类型的 DMX 查询（包括许多类型的预测查询）。 提供了针对内容查询、使用嵌套数据集的查询、从挖掘结构返回事例的查询以及数据定义查询的模板。  
  
-   MDX 和 DMX 查询窗格中的元数据资源管理器提供了可用模型和结构（可将其拖放到查询生成器中）的列表以及 DMX 函数的列表。 可利用此功能轻松地获取正确的对象名，而无需键入。  
  
 本主题介绍如何通过使用元数据资源管理器和 DMX 查询编辑器来生成 DMX 查询。  
  
##  <a name="BKMK_Templates"></a> DMX 查询模板  
 模板资源管理器中有创建 DMX 基本查询的模板。 **DMX** 文件夹包含数据挖掘模板，这些模板划分为以下类别：  
  
-   **模型内容**  
  
-   **模型管理**  
  
-   **预测查询**  
  
-   **结构内容**  
  
 还可以为经常运行的查询或命令创建自定义模板。  
  
## <a name="xmla-query-templates"></a>XMLA 查询模板  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 还提供了 XMLA 查询模板。  
  
 可使用 XMLA 和 DMX 执行的查询类型之间存在某种重叠。 例如，可通过使用 DMX 或数据挖掘架构行集创建一些模型内容查询，但是架构行集有时包含不在 DMX 内容查询显示的信息。  
  
 DMX 和 XMLA 中处理操作的方式之间也存在一些关键差异。 例如，可使用 XMLA 执行管理操作（例如，备份整个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库），但如果需要备份单个挖掘模型，则 DMX 会提供一个简单命令 [EXPORT (DMX)](/sql/dmx/export-dmx)，使用该命令执行此操作更佳。  
  
##  <a name="BKMK_Building_Queries"></a> 生成和运行 DMX 查询  
  
#### <a name="open-a-new-dmx-query-window"></a>打开新的 DMX 查询窗口  
  
1.  在 **中单击** “新建查询” [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，再选择 **“新建 Analysis Server DMX 查询”**。  
  
2.  出现 **“连接到服务器”** 对话框后，选择包含要使用的挖掘模型的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例。  
  
#### <a name="open-template-explorer"></a>打开模板资源管理器  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，在 **“视图”** 菜单上选择 **“模板资源管理器”**。  
  
2.  单击 **Analysis Server** 可以查看应用于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的模板的树视图。  
  
#### <a name="apply-a-template-to-build-a-query"></a>应用模板以生成查询  
  
-   右键单击适当的查询类型，然后选择“打开”。  
  
-   或者，将模板拖入查询编辑器中。  
  
-   也可以使用 **“查询”** 菜单中的 **“指定参数的值”** 选项来填写查询的参数。  
  
 有关如何从模板创建特定类型的查询的示例，请参阅下列主题：  
  
 [通过模板创建单独预测查询](create-a-singleton-prediction-query-from-a-template.md)  
  
 [针对挖掘模型创建内容查询](create-a-content-query-on-a-mining-model.md)  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘查询接口](data-mining-query-tools.md)   
 [数据挖掘扩展插件 (DMX) 参考](/sql/dmx/data-mining-extensions-dmx-reference)  
  
  
