---
title: 使用报表 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- displaying reports
- overriding reports
- Upgrade Advisor Report Viewer
- reports [Upgrade Advisor], about reports
- formatting reports
- resolved issues [Upgrade Advisor]
- distributing reports [Reporting Services]
- filtering reports [Reporting Services]
- removing report items
- viewing reports
- rerunning analysis
- information issues [Upgrade Advisor]
- deleting report items
- icons [Upgrade Advisor]
- Upgrade Advisor [SQL Server], reports
- sending reports
- blocking issues [Upgrade Advisor]
- sharing reports
- reports [Upgrade Advisor]
- SQL Server Upgrade Advisor, reports
- modifying reports
- distributing reports [Reporting Services], about report distribution
- warnings [Upgrade Advisor]
- analyzing system [Upgrade Advisor], reports
ms.assetid: 4a3cb94a-a7ac-4cec-94c7-db26fcf6d161
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fc3a08e707f6b51059145c69fdee15f78c933135
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66091231"
---
# <a name="using-reports"></a>使用报表
  系统会针对每个组件生成单独的报表，并且必要时会为升级顾问分析向导在服务器上分析的每个实例生成单独的报表。 报表用于提供有关影响升级的已知问题的详细信息。 它还提供指向信息的链接，并提供用于解决确定的问题的建议操作。  
  
> [!NOTE]  
>  如果升级顾问报表查看器在默认报表目录中找不到任何报表，则可以使用 "**打开报表**" 链接从其他目录加载报表。  
  
## <a name="viewing-reports"></a>查看报表  
 可以使用升级顾问报表查看器来查看升级顾问报表。 若要查看报表，请在升级顾问起始页上，单击 "**启动升级顾问报表查看器**"。  
  
 为服务器加载报表后，可选择要查看其升级问题的组件。 你可以从 "**筛选依据**" 框中应用筛选器以查看以下内容：  
  
-   所有问题  
  
-   所有升级问题  
  
-   升级前的问题  
  
-   所有迁移问题  
  
-   已解决的问题  
  
-   未解决的问题  
  
 如果报表的问题超过20个，可通过单击问题列表顶部或底部的 "**后 20**个" 或 "**前 20**个"，移到下一个或上一组问题。  
  
 通过从 "**报表**" 下拉列表框中选择报表，可以查看最多五个已保存的报表。 这些报表是按其生成时间戳列出的。  
  
## <a name="report-format"></a>报表格式  
 报表查看器分三列显示报表问题。 每个问题均可折叠，以便您能够隐藏说明并仅查看关键信息。  
  
 第一列是**重要性**列。 图标指示的是每一问题的重要性，对于阻塞问题或重要问题，显示带 X 的红色圆圈，而对于警告问题和供参考的信息，则显示带感叹号的黄色三角形。 第二列是**修复的时间**，指示何时必须解决问题。 您可以对报表的**重要性**或**修改时间**进行排序。 第三列 "**说明**" 列出了问题的标题。  
  
 展开某一问题后，可显示相应的附加信息、指向有关如何解决该问题的详细信息的链接以及指向显示问题详细信息的链接。 在单击用以获取该问题的详细信息的链接后，将会显示一个帮助主题，其中显示有关该问题的信息以及有关如何解决该问题的信息。 解决问题或管理操作项后，可以通过选中 "**此问题已解决**" 复选框，将问题标记为完成。 如果要从升级问题列表中删除已解决的问题，请单击 "**刷新**"。 在对同一组件运行升级顾问分析向导或从 "**筛选依据**" 选项应用 "**已解决的问题**" 筛选器之前，不会再次显示此问题。  
  
## <a name="report-files"></a>报表文件  
 升级顾问分析向导会在 My Documents\\ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Upgrade Advisor\110\Reports 目录中创建报告，并为您分析的每个服务器创建一个子目录。 报表文件为遵循特定的命名约定的 XML 文件。 启动升级顾问报表查看器后，将显示默认目录中的报表文件。 如果要将报表文件复制到此文件夹，则报表文件必须遵循相应的命名约定，否则报表查看器不会自动显示这些报表文件。  
  
 如果您希望与他人共享信息，可向他们发送 XML 报表。 或者，如果您希望使用其他应用程序，可将报表导出为可用于创建电子表格、文本文件或电子邮件的逗号分隔值文件。  
  
## <a name="see-also"></a>另请参阅  
 [如何查看升级顾问报表](../../../2014/sql-server/install/how-to-view-an-upgrade-advisor-report.md)   
 [如何：导出报表](../../../2014/sql-server/install/how-to-export-reports.md)   
 [如何：筛选报表](../../../2014/sql-server/install/how-to-filter-reports.md)   
 [解决升级问题](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [SQL Server 2014 升级顾问 &#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
