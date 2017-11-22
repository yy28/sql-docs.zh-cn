---
title: "创建链接域 | Microsoft Docs"
ms.custom: 
ms.date: 11/08/2011
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: 
ms.component: data-quality-services
ms.reviewer: 
ms.suite: sql
ms.technology: data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.dqs.kb.linkeddomain.f1
ms.assetid: fd99d422-c53d-4d7c-9cdd-303c703683b6
caps.latest.revision: "20"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 898177d27b1c580d8cf40f6d2966ab91c7b01733
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="create-a-linked-domain"></a>创建链接域
  本主题描述如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 的知识库中创建链接域。 链接域可以从先前存在的另一个域创建，并且继承它所链接到的域的所有值、规则和属性，但名称和说明除外。 您可以将一组链接域作为一个链接域进行管理。 通过将一个域链接到另一个域，您可以创建从另一个域继承其内容的域。  
  
## <a name="scenarios"></a>方案  
 链接域在下列情况下尤其有用。  
  
### <a name="mapping-multiple-fields-to-domains-that-share-values-rules-and-properties"></a>将多个字段映射到共享值、规则和属性的域  
 您无法将两个字段映射到同一个域，但您可以将一个字段映射到一个域，然后将第二个字段映射到已链接到第一个域的域。 这样就将字段映射到具有相同内容和属性（名称和说明除外）的两个不同域。 有关详细信息，请参阅 [Map two fields to linked domains](#Map)。  
  
### <a name="controlling-data-flow-to-composite-domains"></a>控制到复合域的数据流  
 链接域使您能够控制字段与复合域之间的数据流。 您可以区分一个字段中的数据何时流向复合域，而另一个非常相似的域中的数据何时不流向复合域。 这是通过指定以下内容来实现的：在两个链接域中，一个域是复合域的一部分，而另一个域则不是。 从域角度来看，链接域是完全相同的。 它们包含同样的知识。 然而，从复合域的角度来看，链接域是不同的。 一个参与复合域；另一个则不参与。  
  
 例如，一条包含以下字段的记录：Customer First Name、Customer Last Name 和 Father’s First Name。 假设您同时将客户的名字和父亲的名字映射到 First Name 域，并使 First Name 域和 Last Name 域成为 Full Name 复合域的组成部分。 问题是父亲的名字将添加到复合域，但没有姓氏。 但是，如果您将这两个名字字段链接到一个域并链接这两个域，则您可以将 Customer First Name 域链接到 Full Name 复合域，但不将 Father’s First Name 字段添加到复合域；从而防止将 Father’s First Name 添加到复合域。  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Prerequisites"></a> 先决条件  
 若要创建链接域，您必须具有知识库和要链接到的现有域。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 权限  
 您必须对 DQS_MAIN 数据库具有 dqs_kb_editor 或 dqs_administrator 角色，才能创建链接域。  
  
##  <a name="Create"></a> 创建链接域  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 的主屏幕中，打开或创建一个知识库。 选择 **“域管理”** 作为活动，然后单击 **“打开”** 或 **“创建”**。 有关详细信息，请参阅 [创建知识库](../data-quality-services/create-a-knowledge-base.md) 或 [打开知识库](../data-quality-services/open-a-knowledge-base.md)。  
  
3.  从 **“域管理”** 页上的 **“域列表”** 中，右键单击您要将新域链接到的域，然后单击 **“创建链接域”**。  
  
    > [!NOTE]  
    >  没有专门用于创造链接域的图标。 您只能使用上下文菜单中的命令。  
  
4.  在 **“创建域”** 对话框中，输入名称（对知识库唯一）以及说明（最多 256 个字符）。 验证所链接到的域的名称是正确的。  
  
5.  单击 **“确定”** 完成创建链接域。  
  
6.  如有必要，您可以在“域属性”选项卡中更改链接域的名称或说明。  
  
7.  单击 **“完成”** 以完成域管理活动，如 [End the Domain Management Activity](http://msdn.microsoft.com/library/ab6505ad-3090-453b-bb01-58435e7fa7c0)中所述。  
  
##  <a name="Map"></a> Map two fields to linked domains  
  
1.  为知识发现活动打开一个知识库，并将此知识库映射到数据库以及表或视图。  
  
2.  将一个字段映射到域，然后尝试将第二个字段映射到同一个域。  
  
3.  在指示域已在使用的弹出式窗口中，单击“是”以创建链接域。  
  
4.  在“创建域”对话框中，输入名称和说明，然后单击“确定”。  
  
##  <a name="FollowUp"></a> 跟进：创建链接域后  
 在创建链接域后，您可以对域执行其他域管理任务，可以执行知识发现以便向域添加知识，或者可以向域添加匹配策略。 有关详细信息，请参阅[执行知识发现](../data-quality-services/perform-knowledge-discovery.md)、[管理域](../data-quality-services/managing-a-domain.md)或[创建匹配策略](../data-quality-services/create-a-matching-policy.md)。  
  
##  <a name="Behavior"></a> 链接域的行为  
 可以更改链接域的设置，如下所示：  
  
-   您可以更改链接域的名称和说明。  
  
-   若要更改 **“数据类型”**、 **“使用前导值”**或 **“将输出格式设置为”** 属性，请选择链接到的域，然后在该域的 **“域属性”** 选项卡中更改这些设置。 您不能在链接域的属性中更改这些设置。 有关详细信息，请参阅 [创建域](../data-quality-services/create-a-domain.md)。  
  
-   可以针对链接域或它链接到的域更改“域管理”页的 **“引用数据”**、 **“域规则”**、 **“域值”**和 **“基于字词的关系”** 选项卡中的设置，并且这些更改将被另一个域继承。  
  
 链接域具有以下特征：  
  
-   您不能取消两个域的链接。 要删除链接，请删除其中一个链接域。  
  
-   当您在“域管理”页的域列表中选择链接域时，在包含 **“值”** 表的窗格中标识链接域的字符串包括指示该域为链接域的内容。  
  
-   如果您删除一个域所链接到的域，这两个域都将被删除。 但是，您可以删除链接域，而不删除所链接到的域。  
  
-   链接域无法链接到自身已链接到其他域的域。  
  
-   无法为复合域创建链接域或链接复合域。  
  
-   当在任意一个“域管理”选项卡上双击链接域时，将打开该域以供编辑，并且名称字符串中指示该域为链接域。  
  
  
