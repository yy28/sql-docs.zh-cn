---
title: 在复合域中使用值关系 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.dm.cdvaluerelations.f1
ms.assetid: 5ee468f0-8538-4620-90e8-63f466c9000e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d26836ca62c4a86cfbfde5b7f29920911ac6efdf
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48081857"
---
# <a name="use-value-relations-in-a-composite-domain"></a>在复合域中使用值关系
  本主题介绍如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 知识发现过程中查看为复合域找到的值组合。 此页显示值组合的出现次数。 复合域不支持值管理，因此，您无法对这些值执行任何操作。  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Prerequisites"></a> 先决条件  
 若要查看值关系，您必须创建并打开了一个复合域。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 您必须对 DQS_MAIN 数据库具有 dqs_kb_editor 或 dqs_administrator 角色，才能在复合域中查看值关系。  
  
##  <a name="Use"></a> 查看值关系  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../../2014/data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 的主屏幕中，打开或创建一个知识库。 选择 **“域管理”** 作为活动，然后单击 **“打开”** 或 **“创建”**。 有关详细信息，请参阅 [创建知识库](../../2014/data-quality-services/create-a-knowledge-base.md) 或 [打开知识库](../../2014/data-quality-services/open-a-knowledge-base.md)。  
  
3.  从 **“域管理”** 页上的 **“域列表”** 中，选择您要为其创建域规则的复合域，或者创建一个新的复合域。 如果您必须创建一个新域，请参阅[创建复合域](../../2014/data-quality-services/create-a-composite-domain.md)。  
  
4.  单击 **“查看关系”** 选项卡。  
  
5.  查看为每个值组合显示的频率。  
  
    > [!NOTE]  
    >  **“值”** 表显示在复合域中存在的每个值组合。 每个值都显示在它应用于的单一域中。 值关系表的默认排序是按频率，但您可以单击其他列以便按该列排序。 仅显示其频率大于或等于 20 的那些值。  
  
6.  您不能更改该表中的任何值。 如果您已执行了其他操作，则单击 **“完成”** 可完成域管理活动。 否则，单击 **“取消”**。  
  
##  <a name="FollowUp"></a> 跟进：在查看值关系后  
 在查看值关系后，您可以对域执行其他域管理任务，可以执行知识发现以便向域添加知识，或者可以向域添加匹配策略。 有关详细信息，请参阅[执行知识发现](../../2014/data-quality-services/perform-knowledge-discovery.md)、[管理域](../../2014/data-quality-services/managing-a-domain.md)或[创建匹配策略](../../2014/data-quality-services/create-a-matching-policy.md)。  
  
  
