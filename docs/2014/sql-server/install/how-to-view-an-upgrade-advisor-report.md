---
title: 如何查看升级顾问报表 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- displaying reports
- viewing reports
- Upgrade Advisor [SQL Server], reports
- SQL Server Upgrade Advisor, reports
- reports [Upgrade Advisor], viewing
ms.assetid: d13b38af-0ac3-4030-83cd-e7d7825dd09f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c0ae231e380530f11d4c97a917927ed62e99fb47
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66094797"
---
# <a name="how-to-view-an-upgrade-advisor-report"></a>如何查看升级顾问报表
  升级顾问会为选择分析的每个组件创建报表。 本主题说明如何从升级顾问起始页中查看升级顾问报表。  
  
> [!IMPORTANT]  
>  报表查看器基于标准文件名加载文件。 如果文件已重命名，报表查看器将不会加载这些文件。  
  
### <a name="to-view-a-report"></a>查看报表  
  
1.  依次单击 "**开始**"、"**所有程序**"、 **[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]**，然后单击** [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] "升级顾问**"。  
  
2.  在升级顾问起始页上，单击 "**启动升级顾问报表查看器**"。  
  
3.  选择位于计算机中的默认位置的报表：  
  
    1.  在 "**服务器**" 列表中，选择服务器。  
  
    2.  在 "**实例" 或 "组件**" 列表中，选择组件或组件/实例组合。  
  
     选择其他位置上的报表：  
  
    1.  单击 "**打开报表**" 链接。  
  
    2.  找到该报表位置，然后双击 XML 文件。  
  
     升级顾问存储最多五个以前的分析报表作为历史记录。 若要查看这些报表，请单击 "**报表**" 下拉列表框，然后选择报表。 这些报表是按其生成时间戳列出的。  
  
     该报表包含以下有关所有检测到的问题的详细信息：  
  
    -   **重要性**，指示修复问题的重要程度。  
  
    -   **解决时间**，它指示在升级到之前或之后（或必须）升级到[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、迁移应用程序或数据之前或之后，或在任何时间迁移之后。  
  
    -   对问题的简短说明。  
  
4.  如果报表包含的项超过 20 个，请单击报表顶部或底部的绿色前进箭头查看下一组项。 单击绿色的后退按钮可查看前 20 项。  
  
5.  若要对报表进行排序，请单击列标题。  
  
6.  若要查看特定项的详细信息，请单击该项。 将会出现该问题的说明以及其他选项：  
  
    -   若要查看发现此问题的对象，请单击 "**显示受影响的对象**"。  
  
    -   若要查看有关问题的帮助，请单击 "**告诉我有关此问题的详细信息以及如何解决**"。  
  
    -   若要将问题标记为已解决，这会在再次查看报表时隐藏问题，请选择 "**此问题已解决**"。  
  
> [!NOTE]  
>  该报表可能包含与无法检测的问题有关的项。 这些问题是那些无法检测到的问题或会产生太多的误报结果的问题。 单击 "**告诉我有关此问题的详细信息以及如何解决此问题**" 链接，以查看组件的无法检测的问题的列表。  
  
## <a name="see-also"></a>另请参阅  
 [如何：导出报表](../../../2014/sql-server/install/how-to-export-reports.md)   
 [如何：运行升级顾问分析向导](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [解决升级问题](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [升级顾问操作指南主题](../../../2014/sql-server/install/upgrade-advisor-how-to-topics.md)   
 [使用升级顾问](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
