---
title: 将计划的策略部署到多个实例 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f551b8e8-3668-4ed4-852f-bae826254f4f
caps.latest.revision: 6
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: ebabe1d982f427002eea31f09541cd40654bcfc1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37249527"
---
# <a name="deploy-scheduled-policies-to-multiple-instances"></a>将计划的策略部署到多个实例
  通过使用已注册的服务器，可以从一个集中位置将计划的策略部署到多个托管服务器。 您可以从本地服务器组或中央管理服务器部署计划的策略。  
  
 在本任务中，您将执行以下操作：  
  
1.  将您在前一个任务中计划的策略导出到某个文件夹。  
  
2.  将计划的政策部署到通过已注册服务管理的目标实例。  
  
 您将在完成本课程先前任务的计算机上执行这些任务。  
  
## <a name="prerequisites"></a>必要條件  
 此任务具有以下必备条件：  
  
-   您必须完成了本课程中的先前任务。  
  
-   您要在其中部署计划策略的实例必须运行于 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 或更高版本上。 自动过程要求在本地存储策略，但早于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 版本不支持此功能。  
  
-   你想要部署计划的策略的服务器必须在已注册的服务器中注册中任意一种**本地服务器组**或**中央管理服务器**节点。 有关详细信息，请参阅以下主题：  
  
    -   [创建或编辑服务器组 (SQL Server Management Studio)](../ssms/register-servers/create-or-edit-a-server-group-sql-server-management-studio.md)  
  
    -   [注册连接的服务器&#40;SQL Server Management Studio&#41;](../ssms/register-servers/register-a-connected-server-sql-server-management-studio.md)。  
  
    -   [创建中央管理服务器和服务器组 (SQL Server Management Studio)](../ssms/register-servers/create-a-central-management-server-and-server-group.md)  
  
### <a name="to-export-the-scheduled-policies-as-xml-files"></a>将计划策略导出为 .xml 文件  
  
1.  在你在上一任务中配置计划的策略服务器上，展开**管理**，展开**策略管理**，然后单击**策略**。  
  
2.  在“视图”菜单中，单击“对象资源管理器详细信息”。  
  
3.  在中**对象资源管理器详细信息**窗格中，选择所有计划的最佳实践策略，你想要将部署到通过已注册的服务器的其他服务器。  
  
    > [!NOTE]  
    >  可以单击**类别**标题以按类别对策略进行排序。  
  
4.  右键单击所选内容，然后依次**导出策略**。  
  
5.  如果选择了多个策略要导出，请在**浏览文件夹**对话框中，选择目标文件夹，或创建一个新文件夹。 对于本课程中，创建新文件夹，路径**C:\Scheduled_BP_Policies**，然后单击**确定**。  
  
     如果只选择了一个要导出，请在策略**导出策略**对话框框中，使用路径创建一个新文件夹**C:\Scheduled_BP_Policies**，单击**打开**，然后单击**保存**。  
  
     将在此文件夹位置中创建 .xml 策略文件。  
  
### <a name="to-deploy-the-scheduled-policies-to-servers-that-are-managed-through-registered-servers"></a>将计划的政策部署到通过已注册服务管理的服务器  
  
1.  在“视图”菜单上，单击“已注册的服务器”。  
  
2.  展开**数据库引擎**，展开**本地服务器组**或**中央管理服务器**，右键单击你想要部署的策略，该节点，然后单击**导入策略**。  
  
    > [!NOTE]  
    >  如果您右键单击**本地服务器组**或中央管理服务器本身，则策略将部署到所有被管服务器。 如果右键单击特定的服务器组，则策略将只部署到该组中的服务器。 如果右键单击特定的已注册服务器，则策略将只部署到该服务器。  
  
3.  下一步**文件导入**，单击省略号按钮 (**...**).  
  
4.  在中**选择策略**对话框中，浏览到保存计划的策略的文件夹位置。 对于此示例中，浏览到位置**C:\Scheduled_BP_Policies**。  
  
5.  选择你想要导入到目标实例，然后单击策略**打开**。  
  
6.  在中**导入**对话框中**策略状态**列表中，选择所需的策略状态。 您可以选择在导入时保留策略状态、启用或禁用策略。 请注意，必须启用策略才能根据计划运行它们。  
  
7.  单击**确定**将策略导入到目标的所有实例。  
  
    > [!NOTE]  
    >  如果有任何错误**导入**对话框不会消失。 单击**日志**页后，可以查看的消息。 单击**取消**以关闭对话框。  
  
8.  若要查看从目标实例的策略，连接到的实例，打开对象资源管理器，展开**管理**，然后展开**策略**。 您应看到在导入的策略**策略**节点。 如果您双击每个策略，则可以查看计划或更改设置。  
  
    > [!NOTE]  
    >  若要在运行计划的策略之后查看评估结果，请打开目标实例上的“策略历史记录”日志。 若要打开日志，请右键单击**策略管理**，然后单击**查看历史记录**。  
  
## <a name="summary"></a>“摘要”  
 本教程介绍了如何针对 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的一个或多个实例执行最佳实践策略的按需和计划评估。  
  
## <a name="next"></a>Next  
 现已学完了本教程。 若要返回到开始位置，请参阅[教程： 评估基于策略的管理的最佳实践](../../2014/tutorials/tutorial-evaluating-best-practices-by-using-policy-based-management.md)。  
  
 若要查看一系列[!INCLUDE[ssDE](../includes/ssde-md.md)]教程中，单击[数据库引擎教程](../relational-databases/database-engine-tutorials.md)。  
  
## <a name="see-also"></a>请参阅  
 [使用基于策略的管理来管理服务器](../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
