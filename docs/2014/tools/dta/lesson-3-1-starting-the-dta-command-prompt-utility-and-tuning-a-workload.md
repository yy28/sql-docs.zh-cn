---
title: 启动 dta 命令提示符实用工具并优化工作负荷 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: f34a5acf-1f3b-4484-a770-6470cb925ab0
caps.latest.revision: 26
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 8400c0ead99718a46844db9c13a4fb5e60a93550
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125257"
---
# <a name="starting-the-dta-command-prompt-utility-and-tuning-a-workload"></a>启动 dta 命令提示实用工具并优化工作负荷
  此任务指导你如何从命令提示符下启动 **dta** 实用工具，查看其帮助，以及使用它优化工作负荷。 此任务将使用在数据库引擎优化顾问图形用户界面 (GUI) 练习 [优化工作负荷](lesson-1-1-tuning-a-workload.md)中创建的工作负荷 MyScript.sql。  
  
 本教程使用 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 示例数据库。 出于安全原因，默认情况下不安装该示例数据库。 若要安装示例数据库，请参阅 [安装 SQL Server 示例和示例数据库](http://sqlserversamples.codeplex.com)。  
  
 以下任务将指导你打开命令提示符，启动 **dta** 命令提示实用工具，查看其语法帮助，并优化在 [优化工作负荷](lesson-1-1-tuning-a-workload.md)中创建的一个简单工作负荷 MyScript.sql。  
  
### <a name="to-start-the-dta-command-prompt-utility-and-view-help"></a>启动 dta 命令提示实用工具并查看帮助  
  
1.  在“开始”菜单中，依次指向“所有程序”、“附件”，再单击“命令提示符”。  
  
2.  在命令提示符下，键入以下命令，再按 Enter 键：  
  
    ```  
    dta -? | more  
    ```  
  
     该命令的 `| more` 部分是可选的。 但是，使用该选项可以逐页查看实用工具的语法帮助。 按 Enter 键可以按行翻阅帮助文本，按空格键可按页翻阅。  
  
### <a name="to-tune-a-simple-workload-by-using-the-dta-command-prompt-utility"></a>使用 dta 命令提示实用工具优化一个简单的工作负荷  
  
1.  在命令提示符下，导航到存储 MyScript.sql 文件的目录。  
  
2.  在命令提示符下，键入以下命令，然后按 Enter 键运行该命令并启动优化会话（请注意，实用工具分析命令时区分大小写）：  
  
    ```  
    dta -S YourServerName\YourSQLServerInstanceName -E -D AdventureWorks2012 -if MyScript.sql -s MySession2 -of MySession2OutputScript.sql -ox MySession2Output.xml -fa IDX_IV -fp NONE -fk NONE  
    ```  
  
     其中 `-S` 指定安装了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的服务器和 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 实例的名称。 `-E` 设置指定要使用可信连接来连接实例。使用 Windows 域帐户连接时可使用该设置。 `-D` 设置指定要优化的数据库， `-if` 指定工作负荷文件， `-s` 指定会话名称， `-of` 指定该工具要将 [!INCLUDE[tsql](../../includes/tsql-md.md)] 建议脚本写入其中的文件， `-ox` 指定该工具要将 XML 格式的建议脚本写入其中的文件。 最后三个开关指定如下优化选项： `-fa IDX_IV` 指定数据库引擎优化顾问应该只考虑添加索引（包括聚集和非聚集索引）和索引视图； `-fp NONE` 指定分析时不考虑分区策略； `-fk NONE` 指定数据库引擎优化顾问进行建议时不必保留数据库中的现有物理设计结构。  
  
3.  数据库引擎优化顾问完成了优化工作负荷后，将显示一个消息指示优化会话已成功完成。 若要查看优化结果，可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 打开 MySession2OutputScript.sql 和 MySession2Output.xml 文件。 此外，也可以在数据库引擎优化顾问 GUI 中打开 MySession2 优化会话并查看其建议和报告，执行的方式与 [查看优化建议](lesson-1-2-viewing-tuning-recommendations.md) 和 [查看优化报告](lesson-1-3-viewing-tuning-reports.md)中执行的方式相同。  
  
## <a name="summary"></a>“摘要”  
 你已使用 **dta** 实用工具在命令提示符下完成了对一个简单工作负荷的优化。 该工具还提供了其他许多优化选项。 有关详细信息，请参阅工具帮助 (**dta -?**) 和参考主题 [dta 实用工具](dta-utility.md) 。  
  
## <a name="after-you-finish-this-tutorial"></a>学完本教程后  
 学完本教程中的课程后，请参考以下主题来了解有关数据库引擎优化顾问的详细信息：  
  
-   [数据库引擎优化顾问](../../relational-databases/performance/database-engine-tuning-advisor.md) 提供有关如何使用此工具执行任务的说明。  
  
-   [dta 实用工具](dta-utility.md) 提供有关此命令提示实用工具的参考材料和可用于控制此实用工具的操作的可选 XML 文件。  
  
 若要返回教程的起始位置，请参阅 [教程：数据库引擎优化顾问](tutorial-database-engine-tuning-advisor.md)。  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎教程](../../relational-databases/database-engine-tutorials.md)  
  
  