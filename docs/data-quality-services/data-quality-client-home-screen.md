---
title: "Data Quality Client 主屏幕 | Microsoft Docs"
ms.custom: 
ms.date: 02/29/2012
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dqs.clienthome.f1
ms.assetid: 7c6ec469-bc7d-4d19-8e21-11dcf8ade108
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 00ed6a9eaa24ff9981ca4184a7ec8ef3107ffc0f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="data-quality-client-home-screen"></a>数据质量客户端主屏幕
  使用此屏幕可以访问 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 的三组主要任务的用户界面：知识库管理、数据质量项目和管理。  
  
## <a name="options"></a>选项  
  
### <a name="knowledge-base-management"></a>知识库管理  
 DQS 知识库是 DQS 用来提高数据质量的元数据储存库。 该元数据在两个过程中创建：在计算机辅助的知识发现过程中由 DQS 平台创建，以及在交互式的域管理过程中由数据专员创建。  
  
 **新建知识库**  
 启动知识库的创建过程，可以从头创建也可以基于现有知识库的元数据创建。 此命令打开一个页面，您可以在其中标识知识库、使它基于现有知识库、选择所需知识库活动，然后创建知识库。  
  
 **打开知识库**  
 打开知识库，以便您可以管理域、执行知识发现或生成匹配策略。 单击 **“打开知识库”** 按钮将显示 **“打开知识库”** 页，其中显示现有知识库的列表，列出这些知识库的属性、当前状态、知识库及其域的详细信息。 从 **“打开知识库”**页选择一个知识库并打开它。  
  
 **最近的知识库**  
 从屏幕上的列表中，打开一个已创建的知识库。 如果未锁定，请单击向右箭头，然后选择要在（“域管理”、“知识发现”或“匹配策略”）中启动知识库的活动。  
  
 您可以打开锁定的知识库并仅在您锁定它的情况下进行编辑。 如果这样，知识库将以它关闭时的状态打开，该状态在括号中标明。 如果知识库已锁定但是不是您锁定的，则只能以只读方式打开它。  
  
### <a name="data-quality-projects"></a>数据质量项目  
 数据质量项目是 DQS 同时通过计算机辅助数据更正和交互式数据清理来执行数据清理或数据匹配的过程。  
  
 **新建数据质量项目**  
 启动创建新项目的项目。 此命令打开一个页面，您可以在其中标识项目、将它与知识库关联、显示知识库的详细信息、选择所需项目活动，然后创建项目。  
  
 **打开数据质量项目**  
 打开项目，以便您可以执行数据清理或数据匹配。 单击 **“打开数据质量项目”** 按钮将显示 **“打开数据质量项目”** 页，其中显示现有项目的列表，列出这些项目的属性、当前状态、知识库及其域和匹配策略规则的详细信息。 从 **“打开数据质量项目”**页选择一个项目，然后打开它。  
  
 **最近的数据质量项目**  
 从屏幕上的列表中，选择一个已创建的项目。 仅当您锁定它时，才可以打开锁定的项目。 如果这样，项目将以它关闭时的状态打开，该状态在括号中标明。 如果项目已完成，将在活动的“导出”步骤中打开它。  
  
### <a name="administration"></a>管理  
 通过 DQS 管理，您可以监视、配置和维护 DQS。  
  
 **活动监视**  
 显示与所连接的 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]相关的所有活动（当前和历史活动）的状态的视图。 监视的活动类型包括知识管理、数据质量项目和基于 SSIS 的数据更正。  
  
 **配置**  
 显示 Reference Data Services 帐户的配置属性（通过 Windows Azure Marketplace 和直接针对 Reference Data Services）、常规设置（交互式清理、匹配和事件探查）以及日志严重级别设置。  
  
## <a name="see-also"></a>另请参阅  
 [DQS 知识库和域](../data-quality-services/dqs-knowledge-bases-and-domains.md)   
 [数据质量项目 (DQS)](../data-quality-services/data-quality-projects-dqs.md)   
 [DQS 管理](../data-quality-services/dqs-administration.md)  
  
  
