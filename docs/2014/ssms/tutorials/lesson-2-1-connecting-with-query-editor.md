---
title: 连接查询编辑器 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 48725f54-a7b6-4b79-948e-965c1fe4eef1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bcb2454d9f6b4a6df465c33ca218c4a960f8099b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68187820"
---
# <a name="connecting-with-query-editor"></a>连接查询编辑器
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 允许在与服务器断开连接时编写或编辑代码。 当服务器不可用或要节省短缺的服务器或网络资源时，这一点很有用。 您也可以更改查询编辑器与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 新实例的连接，而无需打开新的查询编辑器窗口或重新键入代码。  
  
## <a name="coding-offline"></a>脱机编码  
  
#### <a name="to-write-code-offline-and-then-connect-to-different-servers"></a>脱机编写代码然后连接到其他服务器  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 工具栏上，单击“数据库引擎查询”  以打开“查询编辑器”。  
  
2.  在“连接到数据库引擎”  对话框中，单击“取消”  。 系统将打开查询编辑器，同时，查询编辑器的标题栏将指示您没有连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
3.  在代码窗格中，键入下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句：  
  
    ```  
    SELECT * FROM Production.Product;  
    GO  
    ```  
  
     此时，可以通过依次单击“连接”  、“执行”  、“分析”  或“显示估计的执行计划”  连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例，“查询”  菜单、“查询编辑器”工具栏或在“查询编辑器”窗口中右键单击时显示的快捷菜单中均提供了这些选项。 对于本练习，我们将使用工具栏。  
  
4.  在工具栏上，单击“执行”  按钮，打开“连接到数据库引擎”  对话框。  
  
5.  在“服务器名称”  文本框中，键入服务器名称，再单击“选项”  。  
  
6.  在“连接属性”  选项卡上的“连接到数据库”  列表中，浏览服务器，选择 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]，再单击“连接”  。  
  
7.  若要使用同一个连接打开另一个“查询编辑器”窗口，请在工具栏上单击“新建查询”  。  
  
8.  若要更改连接，请在“查询编辑器”窗口中右键单击，指向“连接”  ，再单击“更改连接”  。  
  
9. 在“连接到 SQL Server”  对话框中，选择 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的另一个实例（如果有），再单击“连接”  。  
  
 您可以利用查询编辑器的这项新功能在多台服务器上轻松运行相同的代码。 这对于涉及类似服务器的维护操作很有效。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [添加缩进](lesson-2-2-adding-indentation.md)  
  
  
