---
title: 管理知识库 | Microsoft Docs
ms.custom: ''
ms.date: 06/04/2013
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 27f306f4-d67c-47f5-b35c-4260cc5d36e3
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 66a1ad8c326dc6fe221777136edcb01a9b9aa1af
ms.sourcegitcommit: c19696d3d67161ce78aaa5340964da3256bf602d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/29/2018
ms.locfileid: "52617487"
---
# <a name="manage-a-knowledge-base"></a>管理知识库

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  本主题介绍如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中对知识库执行管理功能。 您可以删除知识库、对知识库进行解锁、放弃对知识库所做的工作、重命名知识库以及显示其属性。  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Prerequisites"></a> 先决条件  
 若要管理知识库，该知识库必须已创建，并且已发布（如果另一个人创建了此知识库）或已关闭（如果您创建了该知识库）。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 您必须对 DQS_MAIN 数据库具有 dqs_kb_editor 或 dqs_administrator 角色，才能打开知识库。  
  
##  <a name="Manage"></a> 管理知识库  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，单击 **“打开知识库”**。  
  
3.  在知识库表中右键单击某一知识库。  
  
4.  在上下文菜单中，您可以执行以下操作：  
  
    1.  **打开**：单击以便在 **“选择活动”** 窗格中选择的活动中打开该知识库。  
  
    2.  **取消锁定**：如果您是在域管理、知识发现和匹配策略活动的某一步骤中正在使用该知识库的用户，并且关闭了该知识库，则可以取消锁定该知识库。 如果您卸载了该知识库，则其他人士将能够打开并使用该知识库。 如果知识库未处于某一活动状态中，则此命令将不可用。 有关详细信息，请参阅 [Open a Knowledge Base](../data-quality-services/open-a-knowledge-base.md)。  
  
    3.  **放弃工作**：在知识库处于正被使用状态时单击，如表的“状态”字段中的条目所示。 如果知识库未处于某一活动状态中，则此命令将不可用；并且在知识库被锁定时不可用。 有关详细信息，请参阅 [Open a Knowledge Base](../data-quality-services/open-a-knowledge-base.md)。  
  
    4.  **重命名**：单击可使表的“知识库”字段对于您右键单击的知识库而言可编辑。 更改名称，然后单击该知识库和字段中的其他知识库，以便接受名称更改。  
  
    5.  **删除**：单击可从 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]上的 DQS_MAIN 数据库中删除该知识库。  
  
    6.  **属性**：单击可显示数据库的属性，这些属性是只读的。  
  
        1.  **源知识库**：此数据库所基于的知识库。 此为可选项。  
  
        2.  **状态**：指示知识库是否为 **“工作中”** 状态，以及知识库是否处于特定的知识管理活动中，这由其在上次关闭时的状态确定。 该状态可以是 **“工作中”**，在此情况下，知识库在某一知识管理会话中打开，但未处于特定的活动中；也可以是 **“工作中”** 加上知识管理活动，在此情况下，知识库在某一知识管理会话中打开，并且处于特定的活动中。  
  
        3.  **已锁定**：如果知识库已锁定，则为 **True** ；否则为 **False** 。  
  
        4.  **包含未发布的内容**：如果知识库包含尚未通过发布保存的内容，则为 True；否则为 False。  
  
        5.  **锁定方**：关闭了知识库并且锁定它的用户的名称。  
  
        6.  **锁定日期**：锁定时的日期。  
  
        7.  **创建者**：通过其属于的网络创建了知识库的用户的名称。  
  
        8.  **创建日期**：创建时的日期  
  
##  <a name="FollowUp"></a> 跟进：管理知识库后  
 在管理某一知识库后，您的后续步骤取决于您对该知识库执行的操作：  
  
-   如果您打开了该知识库，将继续所选择的活动。  
  
-   如果您取消锁定该知识库，则其他人可以根据指示的状态打开和使用该知识库。  
  
-   如果您放弃对其执行的工作，则该知识库将处于上次发布的状态。  
  
-   如果重命名了该知识库，将需要打开重命名的知识库才能使用它。  
  
-   如果您删除该知识库，将需要选择另一个知识库以便使用，或者创建一个新的知识库。  
  
  
