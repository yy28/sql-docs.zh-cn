---
title: 查看优化报表 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- tuning reports [SQL Server]
ms.assetid: daee6143-269f-428b-8458-9a3e726d586c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4963a309f6c54998ece968f8a5393e818fd30d07
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66110146"
---
# <a name="viewing-tuning-reports"></a>查看优化报表
  在本课程的上一个练习中，您已经查看了在数据库引擎优化顾问建议中创建或删除数据库对象的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本，这些建议是 MySession 优化会话生成的结果。 MySession 优化会话是在 [优化工作负荷](lesson-1-1-tuning-a-workload.md)中创建的。  
  
 尽管查看可用于实现优化结果的脚本时非常有效，但数据库引擎优化顾问仍提供了许多可供查看的有用报告。 这些报告提供了有关正在优化的数据库中现有物理设计结构的信息，以及有关建议的结构的信息。 通过单击“报告”  选项卡可以查看优化报告，如以下练习中所述。 本练习将使用你在[优化工作负荷](lesson-1-1-tuning-a-workload.md)和[查看优化建议](lesson-1-2-viewing-tuning-recommendations.md)中创建的 MySession 和 EvaluateMySession 优化会话。  
  
### <a name="view-tuning-reports"></a>查看优化报告  
  
1.  启动数据库引擎优化顾问。 请参阅 [启动数据库引擎优化顾问](../../relational-databases/performance/database-engine-tuning-advisor.md)。 请确保连接到本课程上一个练习中使用的同一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
     在“会话监视器”  窗格中双击“MySession”  。 数据库引擎优化顾问将加载此会话的会话信息。  
  
2.  单击“报告”  选项卡。  
  
3.  在“优化摘要”  窗格中，可以查看有关此优化会话的信息。 使用滚动条可以查看所有窗格内容。 请注意查看“预期的提高百分比”  和“建议使用的空间”  信息。 设置优化选项时，可以限制建议使用的空间。 在“优化选项”  选项卡上，选择“高级选项”  。 选中“定义建议所用的最大空间”  ，并以 MB 为单位指定建议配置可以使用的最大空间。 使用帮助浏览器中的“后退”  按钮可返回到本教程。  
  
4.  在“优化报告”  窗格中，单击“选择报告”  列表中的“语句开销报告”  。 如果需要更多空间以查看报表，则将“会话监视器”  窗格边框拖动到左侧。 对数据库中的表执行的每个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句都会有相关的性能开销。 通过对表中经常访问的列创建有效的索引，可以降低此性能开销。 此报告显示了在工作负荷中执行语句的原有开销与实现优化建议后的开销相比，估计的提高百分比。 请注意，报告中包含的信息量取决于工作负荷的长度和复杂性。  
  
5.  右键单击网格区域中的“语句开销报告”  窗格，再单击“导出到文件”  按钮。 报表另存为`MyReport`。 文件名后会自动附加 .xml 扩展名。 可以在常用的 XML 编辑器或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中打开 MyReport.xml 以查看报告内容。  
  
6.  返回数据库引擎优化顾问的“报告”  选项卡，并再次右键单击“语句开销报告”  。 查看其他可用选项。 请注意，您可以更改当前查看的报告的字体。 更改此处的字体也会更改其他选项卡式页面上的字体。  
  
7.  单击“选择报告”  列表中的其他报告，了解相关内容。  
  
## <a name="summary"></a>总结  
 现在，你已经浏览了 MySession 优化会话的数据库引擎优化顾问 GUI 的“报告”  选项卡。 可以执行相同的步骤来浏览为 EvaluateMySession 优化会话生成的报告。 双击“会话监视器”  窗格中的 **EvaluateMySession** 开始该会话。  
  
## <a name="next-lesson"></a>下一课  
 [第 3 课：使用 dta 命令提示实用工具](lesson-3-using-the-dta-command-prompt-utility.md)  
  
  
