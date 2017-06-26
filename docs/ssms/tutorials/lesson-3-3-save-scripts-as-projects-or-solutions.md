---
title: "将脚本另存为项目或解决方案 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 72dfd37f-dbe7-4d1d-bda6-7eb54c7922d3
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 5db067d5a2fe5bbf9953484c9a999ed7b1fcddae
ms.openlocfilehash: 3772efa6ab55acd4087cd47f897040f782476636
ms.contentlocale: zh-cn
ms.lasthandoff: 06/23/2017

---
# <a name="lesson-3-3---save-scripts-as-projects-or-solutions"></a>课程 3-3 - 将脚本另存为项目或解决方案
熟悉 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio 的开发人员会喜欢使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的解决方案资源管理器。 您可以将支持您业务的脚本分组为多个脚本项目，然后将各个脚本项目作为一个解决方案进行集中管理。 将脚本置于脚本项目和解决方案中后，便可将其视为一个组同时打开，或者同时保存到 Visual SourceSafe 之类的源代码管理产品中。 脚本项目包括可使脚本正确执行的连接信息，还包括非脚本文件，例如支持文本文件。  
  
以下练习将创建一个可查询 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库的短脚本，该脚本被置于脚本项目和解决方案中。  
  
## <a name="using-script-projects-and-solutions"></a>使用脚本项目和解决方案  
  
#### <a name="to-create-a-script-project-and-solution"></a>创建脚本项目和解决方案  
  
1.  打开 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，然后使用对象资源管理器连接到服务器。  
  
2.  在 **“文件”** 菜单上，指向 **“新建”**，再单击 **“项目”**。 系统将打开“新建项目”对话框。  
  
3.  在“名称”文本框中，键入 **StatusCheck**，在“模板”中单击“SQL Server 脚本”，再单击“确定”以打开新的解决方案和脚本项目。  
  
4.  在解决方案资源管理器中，右键单击“连接”，再单击“新建连接”。 将打开“连接到服务器”对话框。  
  
5.  在“服务器名称”列表框中，键入服务器的名称。  
  
6.  单击“选项”，再单击“连接属性”选项卡。  
  
7.  在“连接到数据库”框中，浏览服务器，选择 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库，再单击“连接”。 包括数据库的连接信息便添加到了项目中。  
  
8.  如果未显示“属性”窗口，请单击解决方案资源管理器中的新连接，然后按 F4。 连接属性将随即显示，并显示有关连接的信息，其中包括作为 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 的“初始数据库”。  
  
9. 在解决方案资源管理器中，右键单击“连接”，再单击“新建查询”。 系统将创建一个名为 **SQLQuery1.sql** 的新查询，该查询连接到你的服务器上的 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库并添加到脚本项目中。  
  
10. 在查询编辑器中，键入以下查询来确定有多少工作订单的结束日期早于开始日期。 （您可以从“教程”窗口中复制和粘贴代码。）  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT COUNT(WorkOrderID)  
    FROM Production.WorkOrder  
    WHERE DueDate < StartDate;  
  
    ```  
  
    > [!NOTE]  
    > 如果需要更多的空间来键入查询，请按 Shift+Alt+Enter 切换到全屏显示模式。  
  
11. 在解决方案资源管理器中，右键单击 **SQLQuery1**，再单击“重命名”。 键入 **Check Workorders****.sql** 作为查询的新名称并按 Enter。  
  
12. 若要保存解决方案和脚本项目，请在“文件”菜单中，单击“全部保存”。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
[摘要：解决方案和脚本项目](../../tools/sql-server-management-studio/lesson-3-4-summary-solutions-and-script-projects.md)  
  
  
  

