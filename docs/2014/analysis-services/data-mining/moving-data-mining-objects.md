---
title: 移动数据挖掘对象 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], models
- data mining editor [Analysis Services]
- mining models [Analysis Services], managing
- Data Mining Designer
- mining models [Analysis Services], modifying
ms.assetid: bc108407-2603-4387-b930-b5bb9df78069
caps.latest.revision: 44
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e538d9769991772b66050cf97e458de86a16830a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37234317"
---
# <a name="moving-data-mining-objects"></a>移动数据挖掘对象
  移动数据挖掘对象的最常见情形是将模型从测试或分析环境部署到生产环境，或者与其他用户共享模型。  
  
 本主题介绍如何使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]提供的工具和脚本撰写语言来移动数据挖掘对象。  
  
## <a name="moving-data-mining-objects-between-databases-or-servers"></a>在数据库或服务器之间移动数据挖掘对象  
 您可以通过以下方法在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库之间或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例之间移动数据挖掘对象：  
  
-   将解决方案重新部署到其他数据库。  
  
-   撰写单独对象的脚本。  
  
-   备份然后还原分发数据库的副本。  
  
-   导出和导入结构和模型。  
  
 下一节更为详细地说明这些选项。  
  
### <a name="deploying"></a>部署  
 将解决方案部署到不同的服务器或数据库要求您具有以前通过使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]创建的解决方案文件。  
  
 有关部署 Analysis Services 解决方案的详细信息，请参阅[部署 Analysis Services 项目 (SSDT)](../multidimensional-models/deploy-analysis-services-projects-ssdt.md)。  
  
### <a name="scripting"></a>脚本编写  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供了几种语言，可用于撰写对象的脚本。  
  
-   **XMLA**：可以通过在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中右键单击对象，使用 XMLA 编写对象的脚本。 若要执行该脚本，请在目标服务器上的 **“XMLA 查询”** 窗口中打开该脚本。  
  
-   **DMX**：您可以通过使用模板或在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中提供的查询生成器之一创建脚本。  
  
 但请注意，在您可以使用各脚本撰写语言执行的任务之间存在差异：  
  
-   诸如对象说明和数据绑定之类的属性只能通过使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DDL 语言创建或更改，使用 DMX 则不可以。  
  
-   只有 DMX 支持导入和导出挖掘对象。  
  
-   只有 DMX 支持生成 PMML 或从 PMML 导入模型定义。  
  
-   只有 DMX 支持使用应用程序数据对模型定型。 此外，DMX INSERT INTO 语句支持在不为键列提供值的情况下为模型定型。  
  
 有关详细信息，请参阅[使用 Analysis Services 脚本语言 (ASSL) 开发](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)。  
  
### <a name="backup-and-restore"></a>备份和还原  
 备份和还原整个 Analysis Services 数据库是在数据挖掘解决方案依赖于 OLAP 对象的情况下选择的方法。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 提供了备份和还原功能，可以更快、更方便地备份数据库。  
  
 有关备份的详细信息，请参阅 [备份和还原 Analysis Services 数据库](../multidimensional-models/backup-and-restore-of-analysis-services-databases.md)。  
  
### <a name="exporting-and-importing"></a>导出和导入  
 导出后再导入挖掘模型和结构（使用 DMX 语句）是最简单的移动或备份各关系数据挖掘对象的方法。 有关这些操作的 DMX 语法的详细信息，请参阅以下主题：  
  
-   [导出&AMP;#40;DMX&AMP;#41;](/sql/dmx/export-dmx)  
  
-   [导入&AMP;#40;DMX&AMP;#41;](/sql/dmx/import-dmx)  
  
 如果指定 INCLUDE DEPENDENCIES 选项， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 还将导出所有所需数据源视图的定义，并且将在导入模型或结构时在目标服务器上重新创建数据源视图。 完成了模型导入后，请确保对对象设置必需的挖掘权限。  
  
> [!NOTE]  
>  您不能使用 DMX 导出和导入 OLAP 模型。 如果挖掘模型基于 OLAP 多维数据集，则必须使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供的功能来备份和还原整个数据库，或者重新部署多维数据集及其模型。  
  
## <a name="see-also"></a>请参阅  
 [管理数据挖掘解决方案和对象](management-of-data-mining-solutions-and-objects.md)  
  
  
