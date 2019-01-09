---
title: 显示估计的执行计划 | Microsoft Docs
ms.custom: ''
ms.date: 11/21/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- zoom [SQL Server]
- estimated execution plan [SQL Server]
- displaying execution plans
- viewing execution plans
- execution plans [SQL Server], displaying
- customizing execution plan display [SQL Server]
- modifying execution plan display
- custom zoom [SQL Server]
ms.assetid: e94aa576-4c0c-4c54-ad05-6c3432cc615b
author: julieMSFT
ms.author: jrasnick
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6f5f10a0a0fb1ce80ad8d6bc5018362669e7f26b
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53372999"
---
# <a name="display-the-estimated-execution-plan"></a>显示估计的执行计划
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  本主题介绍了如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]生成图形化的估计的执行计划。 生成估计的执行计划时， [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询或批处理并不执行。 为此，估计的执行计划不包含任何运行时信息，例如实际的资源使用量度量值或运行时警告。 生成的执行计划显示的是如果实际执行查询 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 最有可能使用的查询执行计划，并显示流经计划中的多个运算符的估计的行。  
  
 为了使用此功能，用户必须具有执行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询（为其生成图形执行计划）的相应权限，并且用户必须获得了对查询引用的所有数据库的 SHOWPLAN 权限。  
  
## <a name="to-display-the-estimated-execution-plan-for-a-query"></a>显示查询的估计的执行计划  
  
1.  在工具栏上，单击 **“数据库引擎查询”**。 通过单击 **“打开文件”** 工具栏按钮，再定位到该现有查询，也可以打开一个现有查询并显示估计的执行计划。  
  
2.  输入您希望为其显示估计的执行计划的查询。  
  
3.  在 **“查询”** 菜单上，单击 **“显示估计的执行计划”** ，或单击 **“显示估计的执行计划”** 工具栏按钮。 估计的执行计划在结果窗格中的 **“执行计划”** 选项卡上显示。 

    ![工具栏上的“估计执行计划”按钮](../../relational-databases/performance/media/estimatedexecplantoolbar.png "Estimated Execution Plan button on toolbar")    

    若要查看其他信息，请将鼠标暂停在逻辑和物理运算符图标上，并查看显示的工具提示中有关运算符的说明和属性。 另外，还可以在“属性”窗口中查看运算符属性。 如果属性不可见，请右键单击一个运算符并单击“属性”。 选择要查看其属性的运算符。  

    ![右键单击计划运算符中的“属性”](../../relational-databases/performance/media/planproperties.png "Right-click Properties in plan operator")    
  
4.  若要更改执行计划的显示，请右键单击“执行计划”并选择“放大”、“缩小”、“自定义显示比例”或“缩放到合适大小”。 “放大”和“缩小”允许你按固定量扩大或减小执行计划。 “自定义缩放” 允许你定义自己的显示放大倍数，例如缩放到 80%。 **“缩放到合适大小”** 会放大执行计划以适应结果窗格。 或者，使用 Ctrl 键和鼠标滚轮的组合来激活动态缩放。  

5.  若要导航执行计划的显示，请使用垂直和水平滚动条，或单击并按住执行计划的任何空白区域，然后拖动鼠标。 或者，在右下角的执行计划窗口中单击并按住加号 (+)，以显示整个执行计划的缩略图。
 
> [!NOTE] 
> 或者，使用 [SET SHOWPLAN_TEXT](../../t-sql/statements/set-showplan-xml-transact-sql.md) 返回语句的执行信息，但不执行语句。 如果在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中使用，“结果”选项卡中将包含用于以图形格式打开执行计划的链接。   
