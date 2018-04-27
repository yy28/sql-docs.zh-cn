---
title: 创建跨域规则 | Microsoft Docs
ms.custom: ''
ms.date: 11/22/2011
ms.prod: sql
ms.prod_service: data-quality-services
ms.service: ''
ms.component: data-quality-services
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dqs.dm.testcdrule.f1
- sql13.dqs.dm.cdrules.f1
ms.assetid: 0f3f5ba4-cc47-4d66-866e-371a042d1f21
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 34ae3b81b3c1ba761647806662f4c146d2fef7c5
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="create-a-cross-domain-rule"></a>创建跨域规则

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  本主题描述如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 的知识库中为复合域创建跨域规则。 跨域规则测试在复合域中包含的单一域中各值之间的关系。 跨域规则必须在复合域中保持正确，这样才能认为域值是准确的并且符合业务要求。 跨域规则用于验证、更正和标准化域值。  
  
 将分别为复合域中的单一域之一定义跨域规则的 If 子句和 Then 子句。 必须为不同的单一域定义每个子句。 跨域规则必须与多个单一域相关；不能为复合域定义简单域规则（仅针对单一域）。 您应该通过为单一域定义域规则来这样做。 If 子句和 Then 子句可分别包含一个或多个条件。  
  
 具有可定义条件的跨域规则将规则逻辑应用于条件中的值的同义词以及这些值本身。 If 和 Then 子句的可定义条件是值等于、值不等于、值处于和值不处于。 例如，假定对于某一复合域，您具有以下跨域规则：“For ‘City’, if Value is equal to ‘Los Angeles’, then for ‘State’, Value is equal to ‘CA’。” 如果‘Los Angeles’ 和 ‘LA’是同义词，则此规则对于‘Los Angeles CA’和‘LA CA’将返回正确结果，对于‘Los Angeles WA’和‘LA WA’将返回错误结果。  
  
 除了让您知道跨域规则的有效性之外，跨域规则 *“值等于”* 中的可定义 **Then**子句还在数据清理活动过程中更正数据。 有关详细信息，请参阅 [Data Correction using Definitive Cross-Domain Rules](../data-quality-services/cleanse-data-in-a-composite-domain.md#CDCorrection) 中的 [Cleanse Data in a Composite Domain](../data-quality-services/cleanse-data-in-a-composite-domain.md)。  
  
 应首先考虑仅影响单一域的所有简单规则，之后才考虑跨域规则。 只有在某个值通过单一域规则（如果它们存在）之后，才会应用跨域规则。 对其运行某个规则的复合域和单一域必须全都定义后，才能执行该规则。  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Prerequisites"></a> 先决条件  
 若要创建一个跨域规则，必须已创建并打开了一个复合域。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 您必须对 DQS_MAIN 数据库具有 dqs_kb_editor 或 dqs_administrator 角色，才能创建跨域规则。  
  
##  <a name="Create"></a> 创建跨域规则  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 的主屏幕中，打开或创建一个知识库。 选择 **“域管理”** 作为活动，然后单击 **“打开”** 或 **“创建”**。 有关详细信息，请参阅 [创建知识库](../data-quality-services/create-a-knowledge-base.md) 或 [打开知识库](../data-quality-services/open-a-knowledge-base.md)。  
  
    > [!NOTE]  
    >  域管理在 Data Quality Service 客户端页面中执行，该页面包含用于单独域管理操作的五个选项卡。 它不是一个向导驱动的过程；任何管理操作都可以单独执行。  
  
3.  从 **“域管理”** 页上的 **“域列表”** 中，选择您要为其创建域规则的复合域，或者创建一个新的复合域。 如果您必须创建新域，请参阅 [Create a Composite Domain](../data-quality-services/create-a-composite-domain.md)。  
  
4.  单击 **“复合域规则”** 选项卡。  
  
5.  单击 **“添加新的域规则”**，然后为该规则输入名称和说明。  
  
6.  选择 **“活动”** 可指定将运行该规则（默认设置），取消选中则可以阻止该规则运行。  
  
7.  按如下所示创建 If 子句：  
  
    1.  在 If 子句窗格中的域列表中，选择在复合域中包括的单一域之一以便作为 If 子句的对象。 您可以选择复合域中的任何单一域。  
  
    2.  从下拉列表中选择某个条件作为子句的第一个条件。  
  
    3.  如果该条件需要值，则在文本框中输入与该条件相关联的值。  
  
    4.  如果 If 子句要求其他条件，则单击 **“向所选子句添加新的条件”**。 选择操作符和条件，并且根据需要为该条件输入值。  
  
    5.  若要更改这些条件的顺序，请通过单击其左侧选择一个条件，再单击向上或向下箭头。  
  
    6.  若要隐藏条件，请单击域名左侧的减号。 单击加号可显示条件。  
  
8.  在 Then 子句窗格的域列表中通过选择并非 If 子句的对象的单一域，创建 Then 子句。 然后，使用与生成 If 子句相同的步骤生成 Then 子句。  
  
9. 继续执行下面的测试过程。  
  
##  <a name="Test"></a> 测试跨域规则  
  
1.  按如下所示测试跨域规则：  
  
    1.  单击复合域窗格右上角中的 **“对测试数据运行所选域规则”** 图标。  
  
    2.  在 **“测试域规则”** 对话框中，单击 **“为域规则添加新的测试字词”** 图标。  
  
    3.  为与 If 子句相关联的单一域以及与 Then 子句相关联的单一域输入测试值。 在 If 子句中输入的测试值必须满足该子句的条件，否则，将在 **“有效性”** 列中输入一个问号，指示跨域规则不应用于测试数据。  
  
    4.  再次单击 **“为域规则添加新的测试字词”** 图标以便添加另一组测试值。  
  
    5.  单击 **“对所有字词测试域规则”** 图标。 如果一组测试值有效，则 DQS 将在 **“有效性”** 列中为该行输入一个复选标记。 如果该组测试值无效，则 DQS 将在“有效性”列中为该行输入一个内含惊叹号的三角形。  
  
    6.  完成测试后，在 **“测试复合域规则”** 对话框中单击 **“关闭”** 。  
  
2.  在完成了您的跨域规则后，单击 **“完成”** 以完成域管理活动，如 [End the Domain Management Activity](http://msdn.microsoft.com/library/ab6505ad-3090-453b-bb01-58435e7fa7c0)中所述。  
  
##  <a name="FollowUp"></a> 跟进：创建跨域规则后  
 在创建跨域规则后，您可以对域执行其他域管理任务，可以执行知识发现以便向域添加知识，或者可以向域添加匹配策略。 有关详细信息，请参阅[执行知识发现](../data-quality-services/perform-knowledge-discovery.md)、[管理域](../data-quality-services/managing-a-domain.md)或[创建匹配策略](../data-quality-services/create-a-matching-policy.md)。  
  
  
