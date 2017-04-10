---
title: "从 .dqs 文件导入知识库 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9b9786fe-9e80-429a-afcb-dc3b3dd6f0b0
caps.latest.revision: 17
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 17
---
# 从 .dqs 文件导入知识库
  本主题介绍如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中从 .dqs 数据文件导入整个知识库。 通过在导出现有知识库创建数据文件 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 应用程序 (请参阅 [将知识库导出到.dqs 文件](../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md))。  
  
 使用 .dqs 数据文件导出知识库的内容，然后将内容导入到同一个 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 或不同 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 中的另一个知识库，可以简化知识生成过程、节省时间并提高效率。 这样，您就可以与他人共享知识库及其知识，同时节省时间。 .dqs 文件将包含所有知识库信息，其中包括域和匹配策略，但附加的引用数据信息除外。 将导入已发布和未发布的数据。  
  
 .dqs 数据文件已加密，因此无法查看。  
  
 在导入知识库时，您可以使用相同的名称，除非客户端应用程序中已存在该知识库名称，在这种情况下，您必须重新命名知识库。  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Prerequisites"></a> 先决条件  
 若要从 .dqs 文件中导入知识库，您必须已将该知识库导出到 .dqs 文件。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 权限  
 您必须对 DQS_MAIN 数据库具有 dqs_kb_editor 或 dqs_administrator 角色，才能从 .dqs 数据文件导入知识库。  
  
##  <a name="Import"></a> 从 .dqs 文件导入知识库  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [运行数据质量客户端应用程序](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，单击 **“新建知识库”**。  
  
3.  输入该知识库的名称。  
  
4.  单击 **“知识库创建自”**的向下箭头，然后选择 **“自 DQS 文件导入”**。  
  
5.  对于 **“选择数据文件”**，单击 **“浏览”**。  
  
6.  在 **“从数据文件导入”** 对话框中，转到包含要导入的 .dqs 文件的文件夹，然后单击该文件的名称。 单击 **“打开”**。  
  
7.  验证 **“域”** 列表中显示正确的知识库和域。  
  
8.  选择要执行的活动，然后单击 **“创建”**。  
  
9. 在 **“导入知识库”** 对话框中，验证状态行是否指示导入已完成。 单击“确定” 。  
  
10. 完成知识发现、域管理或需要执行的匹配策略任务，然后单击 **“完成”**。  
  
11. 单击 **“发布”** 发布知识库中的知识，或单击 **“否”** 不发布知识。  
  
12. 如果您发布知识库，则单击 **“确定”**。  
  
13. 在 Data Quality Services 主页中，验证该知识库是否列在 **“最近的知识库”**下。  
  
##  <a name="FollowUp"></a> 跟进：从 .dqs 文件导入知识库后  
 在从 .dqs 文件导入知识库之后，您可以将知识添加到知识库，或在清理或匹配项目中使用此知识库，具体取决于知识库的内容。 有关详细信息，请参阅 [执行知识发现](../data-quality-services/perform-knowledge-discovery.md), ，[管理域](../data-quality-services/managing-a-domain.md), ，[管理复合域](../data-quality-services/managing-a-composite-domain.md), ，[创建匹配策略](../data-quality-services/create-a-matching-policy.md), ，[数据清理](../data-quality-services/data-cleansing.md), ，或 [数据匹配](../data-quality-services/data-matching.md)。  
  
  