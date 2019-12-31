---
title: 创建数据质量项目
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.dqproject.newdqproject.f1
helpviewer_keywords:
- create,data quality project
- data quality project,create
ms.assetid: 19c52d2b-d28e-4449-ab59-5fe0dc326cd9
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 99b869f153e6dacac799f8630283dbaf8d27660b
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75245490"
---
# <a name="create-a-data-quality-project"></a>创建数据质量项目

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  本主题介绍如何使用 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]创建数据质量项目。 数据质量项目用于在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中运行清理或匹配活动。  
  
##  <a name="BeforeYouBegin"></a>开始之前  
  
###  <a name="Prerequisites"></a>先决条件  
 对于清理或匹配活动，您必须具有要在数据质量项目中使用的相关知识库。  
  
###  <a name="Security"></a>安全  
  
####  <a name="Permissions"></a>访问  
 您必须对 DQS_MAIN 数据库具有 dqs_kb_editor 或 dqs_kb_operator 角色才能创建数据质量项目。  
  
##  <a name="Create"></a>创建数据质量项目  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，单击 **“新建数据质量项目”**。  
  
3.  在 **“新建数据质量项目”** 屏幕中：  
  
    1.  在 **“名称”** 框中，键入新的数据质量项目的名称。  
  
    2.  还可以在 **“说明”** 框中键入新的数据质量项目的说明。  
  
    3.  在 **“使用知识库”** 列表中，单击以便选择要用于数据质量项目的知识库 右侧的“知识库详细信息: <Knowledge_Base_Name>”区域将显示所选知识库中提供的域名****。  
  
    4.  在 **“选择活动”** 区域中，单击您要使用此数据质量项目执行的活动：  
  
        -   **清理**：选择此活动将清理源数据。  
  
        -   **匹配**：选择此活动以执行匹配。 只有在为数据质量项目选择的知识库包含匹配策略的情况下，此活动才可用。  
  
4.  单击 **“创建”** 将创建数据质量项目。  
  
##  <a name="FollowUp"></a>跟进：在创建数据质量项目后  
 在创建数据质量项目后，将向您提供一个向导，可用于执行所选活动：清理或匹配。 有关清理和匹配活动的详细信息，请参阅[数据清理](../data-quality-services/data-cleansing.md)和[数据匹配](../data-quality-services/data-matching.md)。  
  
  
