---
title: 如何：查看升级顾问报表 |Microsoft Docs
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
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66094797"
---
# <a name="how-to-view-an-upgrade-advisor-report"></a>如何：查看升级顾问报表
  升级顾问会为选择分析的每个组件创建报表。 本主题说明如何从升级顾问起始页中查看升级顾问报表。  
  
> [!IMPORTANT]  
>  报表查看器基于标准文件名加载文件。 如果文件已重命名，报表查看器将不会加载这些文件。  
  
### <a name="to-view-a-report"></a>查看报表  
  
1.  单击**启动**，单击**所有程序**，单击**[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]**，然后单击**[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]升级顾问**。  
  
2.  在升级顾问起始页上，单击**启动升级顾问报表查看**。  
  
3.  选择位于计算机中的默认位置的报表：  
  
    1.  在中**Server**列表中，选择一个服务器。  
  
    2.  在中**实例或组件**列表中，选择组件 / 实例组合。  
  
     选择其他位置上的报表：  
  
    1.  单击**打开报表**链接。  
  
    2.  找到该报表位置，然后双击 XML 文件。  
  
     升级顾问存储最多五个以前的分析报表作为历史记录。 若要查看这些报表，请单击**报表**下拉列表框中，然后选择报表。 这些报表是按其生成时间戳列出的。  
  
     该报表包含以下有关所有检测到的问题的详细信息：  
  
    -   **重要性**，指示以解决此问题是非常重要。  
  
    -   **解决**，这表示是否您应 （或必须） 解决此问题之前或之后升级到[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 之前或之后迁移应用程序或数据，或任何时候。  
  
    -   对问题的简短说明。  
  
4.  如果报表包含的项超过 20 个，请单击报表顶部或底部的绿色前进箭头查看下一组项。 单击绿色的后退按钮可查看前 20 项。  
  
5.  若要对报表进行排序，请单击列标题。  
  
6.  若要查看特定项的详细信息，请单击该项。 将会出现该问题的说明以及其他选项：  
  
    -   若要查看的对象找到了此问题，请单击**显示受影响的对象**。  
  
    -   若要查看该问题的帮助，请单击**告诉我有关此问题以及如何解决该问题的详细信息**。  
  
    -   若要将标记为已解决，此问题，将再次查看报表时隐藏该问题，请选择**此问题已得到解决**。  
  
> [!NOTE]  
>  该报表可能包含与无法检测的问题有关的项。 这些问题是那些无法检测到的问题或会产生太多的误报结果的问题。 单击**告诉我有关此问题以及如何解决该问题的详细信息**链接以查看组件无法检测到问题的列表。  
  
## <a name="see-also"></a>请参阅  
 [如何：导出报表](../../../2014/sql-server/install/how-to-export-reports.md)   
 [如何：运行升级顾问分析向导](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [解决升级问题](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [升级顾问操作指南主题](../../../2014/sql-server/install/upgrade-advisor-how-to-topics.md)   
 [使用升级顾问](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
