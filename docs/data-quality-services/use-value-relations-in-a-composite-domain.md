---
title: 在复合域中使用值关系
ms.date: 11/22/2011
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.dm.cdvaluerelations.f1
ms.assetid: 5ee468f0-8538-4620-90e8-63f466c9000e
author: swinarko
ms.author: sawinark
ms.openlocfilehash: e9876e5a232174c387fb46cf4f3b2012f1435dc2
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85883299"
---
# <a name="use-value-relations-in-a-composite-domain"></a>在复合域中使用值关系

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  本主题介绍如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 知识发现过程中查看为复合域找到的值组合。 此页显示值组合的出现次数。 复合域不支持值管理，因此，您无法对这些值执行任何操作。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a>先决条件  
 若要查看值关系，您必须创建并打开了一个复合域。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 您必须对 DQS_MAIN 数据库具有 dqs_kb_editor 或 dqs_administrator 角色，才能在复合域中查看值关系。  
  
##  <a name="view-value-relations"></a><a name="Use"></a>查看值关系  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 的主屏幕中，打开或创建一个知识库。 选择 **“域管理”** 作为活动，然后单击 **“打开”** 或 **“创建”**。 有关详细信息，请参阅 [创建知识库](../data-quality-services/create-a-knowledge-base.md) 或 [打开知识库](../data-quality-services/open-a-knowledge-base.md)。  
  
3.  从 **“域管理”** 页上的 **“域列表”** 中，选择您要为其创建域规则的复合域，或者创建一个新的复合域。 如果您必须创建新域，请参阅 [Create a Composite Domain](../data-quality-services/create-a-composite-domain.md)。  
  
4.  单击 **“查看关系”** 选项卡。  
  
5.  查看为每个值组合显示的频率。  
  
    > [!NOTE]  
    >  **“值”** 表显示在复合域中存在的每个值组合。 每个值都显示在它应用于的单一域中。 值关系表的默认排序是按频率，但您可以单击其他列以便按该列排序。 仅显示其频率大于或等于 20 的那些值。  
  
6.  您不能更改该表中的任何值。 如果您已执行了其他操作，则单击 **“完成”** 可完成域管理活动。 否则，单击 "**取消**"。  
  
##  <a name="follow-up-after-viewing-value-relations"></a><a name="FollowUp"></a> 跟进：在查看值关系后  
 在查看值关系后，您可以对域执行其他域管理任务，可以执行知识发现以便向域添加知识，或者可以向域添加匹配策略。 有关详细信息，请参阅[执行知识发现](../data-quality-services/perform-knowledge-discovery.md)、[管理域](../data-quality-services/managing-a-domain.md)或[创建匹配策略](../data-quality-services/create-a-matching-policy.md)。  
  
  
