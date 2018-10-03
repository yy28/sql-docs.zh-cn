---
title: 使用报表 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
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
ms.openlocfilehash: 0d8ec04baf292807120ed5a26360878ac7e20442
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48070897"
---
# <a name="using-reports"></a>使用报表
  系统会针对每个组件生成单独的报表，并且必要时会为升级顾问分析向导在服务器上分析的每个实例生成单独的报表。 报表用于提供有关影响升级的已知问题的详细信息。 它还提供指向信息和建议的操作进行寻址已确定的问题。  
  
> [!NOTE]  
>  如果升级顾问报表查看器在默认报表目录中未找到任何报表，您可以通过使用，从其他目录加载报表**打开报表**链接。  
  
## <a name="viewing-reports"></a>查看报表  
 可以使用升级顾问报表查看器来查看升级顾问报表。 若要查看报表，在升级顾问起始页，请单击**启动升级顾问报表查看**。  
  
 为服务器加载报表后，可选择要查看其升级问题的组件。 可以应用筛选器从**筛选依据**框，以查看以下信息：  
  
-   所有问题  
  
-   所有升级问题  
  
-   升级前的问题  
  
-   所有迁移问题  
  
-   已解决的问题  
  
-   未解决的问题  
  
 如果报表有超过 20 个问题，您可以通过单击移动到下一个或上一组问题**下一步 20**或**前 20 个**顶部或底部的问题列表。  
  
 可以通过选择从报表中查看最多五个保存的报表**报表**下拉列表框。 这些报表是按其生成时间戳列出的。  
  
## <a name="report-format"></a>报表格式  
 报表查看器分三列显示报表问题。 每个问题均可折叠，以便您能够隐藏说明并仅查看关键信息。  
  
 第一列为**重要性**列。 图标指示的是每一问题的重要性，对于阻塞问题或重要问题，显示带 X 的红色圆圈，而对于警告问题和供参考的信息，则显示带感叹号的黄色三角形。 第二列**解决**，指示当必须解决此问题。 可以对任一报表进行排序**重要性**或**解决**列。 第三列，**说明**，列出了该问题的标题。  
  
 展开某一问题后，可显示相应的附加信息、指向有关如何解决该问题的详细信息的链接以及指向显示问题详细信息的链接。 在单击用以获取该问题的详细信息的链接后，将会显示一个帮助主题，其中显示有关该问题的信息以及有关如何解决该问题的信息。 解决某一问题，或若要管理你的操作项，可以在将通过选择标记为已完成的问题后**此问题已得到解决**复选框。 如果你想要从升级问题的列表中删除已解决的问题，请单击**刷新**。 运行升级顾问分析向导对同一组件或应用之前，该问题才会再次显示**已解决的问题**筛选器从**筛选器通过**选项。  
  
## <a name="report-files"></a>报表文件  
 升级顾问分析向导在我的文档中创建报表\\[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Upgrade Advisor\110\Reports 目录，并创建所分析的每个服务器的子目录。 报表文件为遵循特定的命名约定的 XML 文件。 启动升级顾问报表查看器后，将显示默认目录中的报表文件。 如果要将报表文件复制到此文件夹，则报表文件必须遵循相应的命名约定，否则报表查看器不会自动显示这些报表文件。  
  
 如果您希望与他人共享信息，可向他们发送 XML 报表。 或者，如果您希望使用其他应用程序，可将报表导出为可用于创建电子表格、文本文件或电子邮件的逗号分隔值文件。  
  
## <a name="see-also"></a>请参阅  
 [如何： 查看升级顾问报表](../../../2014/sql-server/install/how-to-view-an-upgrade-advisor-report.md)   
 [如何： 导出报表](../../../2014/sql-server/install/how-to-export-reports.md)   
 [如何： 筛选报告](../../../2014/sql-server/install/how-to-filter-reports.md)   
 [解决升级问题](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [SQL Server 2014 升级顾问&#91;新&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
