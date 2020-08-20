---
description: 创建知识库
title: 创建知识库
ms.date: 06/04/2013
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.kb.selectkb.f1
- sql13.dqs.kb.newkb.f1
ms.assetid: 2733a284-975f-4650-abcc-cc2aad074cab
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 1dd8e0379d25b231de873ccfd1529284e62f0f1d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487896"
---
# <a name="create-a-knowledge-base"></a>创建知识库

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  本主题描述如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中创建知识库，以及如何准备知识库以用于域管理、知识发现或添加匹配策略。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a>先决条件  
 要创建知识库，您必须安装有 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 和 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 您必须对 DQS_MAIN 数据库具有 dqs_kb_editor 或 dqs_administrator 角色，才能创建知识库。  
  
##  <a name="create-a-knowledge-base"></a><a name="Createaknowledgebase"></a> 创建知识库  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，单击 **“新建知识库”**。  
  
3.  输入新知识库的名称和说明。  
  
4.  在 **“创建知识库自”** 中，选择要基于其创建知识库的内容：  
  
    -   如果您不想基于现有知识库或数据文件来创建新知识库，则选择 **“无”** 。  
  
    -   选择 **“现有知识库”** 可以基于已在 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]上创建的知识库或默认知识库来创建新知识库。 从 **“选择知识库”** 下拉列表中选择知识库，或者单击 **“浏览”** 以便显示 **“选择知识库”** 对话框，选择新知识库要基于的一个现有知识库，然后单击 **“确定”**。 在您从 Tablet 中选择一个知识库时，将在该对话框的右侧窗格中显示知识库中的域和匹配规则。 你还可以选择“DQS 数据” **** 知识库，这是默认的知识库，包含与美国公司、地址和有关方数据相关的通用全新域和知识。  
  
    -   选择 **“自 DQS 文件导入”** 将基于 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]上的 DQS 文件创建新的知识库。 单击 **“浏览”**，选择扩展名为 .dqs 的 DQS 数据文件，然后单击 **“确定”**。  
  
5.  在 **“选择活动”** 中，选择要对新知识库执行的活动：  
  
    -   选择 **“域管理”** 可创建知识库并进入您用来修改知识库中的域的屏幕。  
  
    -   选择 **“知识发现”** 可创建知识库并进入一个向导，您可以使用该向导分析数据样本并用分析结果填充知识库的各个域。  
  
    -   选择 **“匹配策略”** 可以创建匹配策略，并将其添加到知识库。  
  
6.  单击“创建”。  
  
##  <a name="follow-up-after-creating-a-knowledge-base"></a><a name="FollowUp"></a> 跟进：在创建知识库后  
 在创建一个知识库后，系统将会向您提供可用于执行知识发现的向导、可用于创建匹配策略的向导或者可用于执行域管理的若干页。 有关知识发现、域管理或匹配策略的详细信息，请参阅[执行知识发现](../data-quality-services/perform-knowledge-discovery.md)[管理域](../data-quality-services/managing-a-domain.md)或[创建匹配策略](../data-quality-services/create-a-matching-policy.md)。  
  
  
