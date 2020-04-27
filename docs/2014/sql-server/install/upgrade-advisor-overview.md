---
title: 升级顾问概述 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor Report Viewer
- SQL Server Upgrade Advisor, components
- tools [Upgrade Advisor]
- Upgrade Advisor [SQL Server], components
- components [Upgrade Advisor]
- Upgrade Advisor Analysis Wizard
- limitations [Upgrade Advisor]
- analyzing system [Upgrade Advisor]
- analyzing system [Upgrade Advisor], about analysis
ms.assetid: f5c56f63-4478-40af-abb9-642f58a0026c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c78630764a26bb8fe281446c1bb997f18d965db7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66091599"
---
# <a name="upgrade-advisor-overview"></a>升级顾问概述
  升级顾问提供了一个中央控制台，可分析 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 和 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 组件，以及查看包含分析结果相关信息的报告。  
  
## <a name="how-upgrade-advisor-works"></a>升级顾问如何工作  
 运行升级顾问时，将显示升级顾问起始页。 升级顾问起始页是以下程序的启动点：  
  
-   升级顾问分析向导  
  
-   升级顾问报表查看器  
  
-   升级顾问帮助  
  
 第一次使用升级顾问时，应运行升级顾问分析向导来分析服务器。 向导完成分析后，请单击向导中的 "**启动报表**" 或返回到升级顾问起始页。 从该起始页中，运行升级顾问报表查看器查看报表。 报表提供的链接内容包含有助于解决已知问题的信息。  
  
## <a name="upgrade-advisor-analysis-wizard"></a>升级顾问分析向导  
 若要执行分析，请单击升级顾问起始页上的 "**启动升级顾问分析向导**"。 升级顾问分析向导收集与计算机、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件以及要分析的跟踪文件有关的信息。 收集并确认所有信息之后，升级顾问分析向导会分析 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件。  
  
> [!NOTE]  
>  每次运行升级顾问分析向导时，都会生成一个独立的报表，而不会覆盖选定组件的现有报表。 但是，报表查看器只显示最近的五个报表。  
  
 当升级顾问分析向导完成分析之后，将分别为分析过程中包括的每个组件创建一个 XML 文件。 XML 文件包含在每个组件中发现的项和问题。  
  
### <a name="what-upgrade-advisor-analyzes"></a>升级顾问的分析内容  
 在每个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件的升级顾问的上下文中都运行有专用分析器。 每个分析器的输出均为针对该组件的 XML 报告。  
  
 升级顾问查询以下 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 组件：  
  
-   数据库服务器（[!INCLUDE[ssDE](../../includes/ssde-md.md)] 联机丛书中也称为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]），它包括 Replication、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理、全文搜索和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
> [!NOTE]  
>  在分析过程中，每个分析器都创建一个日志文件。 可以使用这些日志文件来排除分析故障。 例如，如果升级顾问运行缓慢，可以查看日志文件确定造成拖延的原因。  
  
### <a name="upgrade-advisor-limitations"></a>升级顾问的局限性  
 升级顾问无法检测出可能影响升级的每个问题。 例如，如果您在运行于最终用户桌面的客户端应用程序中嵌入了 SQL 代码，则升级顾问将无法分析此应用程序。 对于这些项，仍必须考虑这些问题并按安装中的要求升级、迁移或修改信息。  
  
 升级顾问不分析加密的存储过程、扩展存储过程中的代码以及使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 以外的语言编写的源代码。  
  
## <a name="upgrade-advisor-report-viewer"></a>升级顾问报表查看器  
 若要查看升级顾问报表，请单击升级顾问起始页上的 "**启动升级顾问报表查看器**"。 升级顾问报表查看器启动时，将加载默认目录中的报表。 如果升级顾问报表查看器在默认目录中未找到任何报表，则不会显示报表。 如果默认目录中没有报表，可以运行升级顾问分析向导来创建报表或从其他服务器或子目录中加载现有报表。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 升级顾问不会覆盖现有报表。 但是，报表查看器只显示最近的五个报表。 若要查看以前的报表，请从 "**报表**" 下拉列表框中选择该报表。 时间戳指示生成报表的日期和时间。  
  
 将升级顾问分析向导生成的 XML 文件加载到升级顾问报表查看器中后，将为每个组件显示一个报告。 该报表包含需要解决的所有已知问题（包括可检测到的问题和无法检测到的问题）。 每个问题都有指示重要性的图标、通知何时必须解决此问题的标签和一个简要说明。 展开问题时，您将看到更详细的说明、问题详细信息链接和帮助文件链接。 每个问题的信息都旨在为您提供充足的信息以便解决此问题。  
  
 大多数组件都存在无法检测到的问题。 若要查看这些问题，请展开组件的 "**其他升级问题**" 项，然后单击链接以查看有关文档中的问题的其他信息。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 向后兼容问题的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书。  
  
## <a name="see-also"></a>另请参阅  
 [使用升级顾问](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
