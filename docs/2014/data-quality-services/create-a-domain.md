---
title: 创建域 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.kb.createdomain.f1
ms.assetid: 5c4828f5-bd51-4c29-b3de-87b7d2f2d3e5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 249e0195d02f0b157e818a0525b0170b0b817b3c
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2018
ms.locfileid: "51031597"
---
# <a name="create-a-domain"></a>创建域
  本主题介绍如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中创建域。 域中的值是字段中数据的语义表示形式。 有关域的详细信息，请参阅[管理域](../../2014/data-quality-services/managing-a-domain.md)。  
  
 可以通过两种方法创建新的域。 第一种方法是在知识发现活动的“映射”步骤期间，当您正在分析数据示例以便将知识添加到新的或现有的知识库中时。 第二种方法是在域管理活动中，当您创建新域（而非更改现有域）时。  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Prerequisites"></a> 先决条件  
 若要创建域，您必须已创建并打开了知识库。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 您必须对 DQS_MAIN 数据库具有 dqs_kb_editor 或 dqs_administrator 角色，才能创建域。  
  
##  <a name="Discovery"></a> 在知识发现活动中创建域  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../../2014/data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，单击 **“打开知识库”** ，然后选择知识库；或单击 **“新建知识库”** 并输入新知识库的属性。  
  
3.  选择 **“知识发现”** 作为活动，然后单击 **“创建”** 以创建新知识库；或单击 **“打开”** 以打开现有知识库。  
  
4.  在 **“映射”** 页上，指定到数据源的连接。 有关详细信息，请参阅 [Perform Knowledge Discovery](../../2014/data-quality-services/perform-knowledge-discovery.md)。  
  
5.  在 **“映射”** 表中，从某个空行的 **“源列”** 列的下拉列表中选择一个源列。 如果相应的域不存在，请单击 **“创建域”** 图标。  
  
##  <a name="DomainManagement"></a> 在域管理活动中创建域  
  
1.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，单击 **“打开知识库”** ，然后选择知识库；或单击 **“新建知识库”** 并输入新知识库的属性。  
  
2.  选择 **“域管理”** 作为活动，然后单击 **“创建”** 以创建新知识库；或单击 **“打开”** 以打开现有知识库。  
  
3.  在 **“域管理”** 页上，单击域列表上方的 **“创建域”** 图标。  
  
##  <a name="Properties"></a> 设置域属性  
  
1.  在 **“创建域”** 对话框中，输入名称（对知识库唯一）以及说明（可多达 256 个字符）。  
  
    > [!NOTE]  
    >  有关域属性的详细信息，请参阅 [Set Domain Properties](../../2014/data-quality-services/set-domain-properties.md)。  
  
2.  在 **“数据类型”** 列表中，选择域中值的数据类型。 数据类型可以是 **String** （默认值）、 **Date**、 **Integer**或 **Decimal**。  
  
3.  选择 **“使用前导值”** 可指定将输出一组同义词中的前导值，而非是其同义词的值。 取消选择 **“使用前导值”** 可指定每个同义词值以其正确或更正形式输出，并且不会被其组的前导值替换。  
  
4.  如果数据类型为 **String**，则选择 **“标准化字符串”** 可删除域值中的特殊字符，这可以改进匹配可能性。  
  
5.  从 **“将输出格式设置为”** 下拉列表中，选择在输出域中的数据值时要采用的格式。 此格式设置特定于在步骤 2 中选择的数据类型，如下面的列表中所示：  
  
    -   对于字符串值，您可以指定字符串将是输出为大写、小写还是首字母大写。  
  
    -   对于日期值，您可以指定日、月和年的格式。  
  
    -   对于整数值，您可以指定要应用的格式掩码的类型。  
  
    -   对于小数值，您可以指定要应用的格式掩码的精确性和类型。  
  
     在 **“将输出格式设置为”** 下拉列表中选择 **“无”** 表示不应用列表中的任何格式。  
  
6.  如果数据类型为 **String**，则在 **“语言”** 下拉列表中，选择您希望应用的拼写检查器的语言版本（如果您启用了拼写检查器）。  
  
7.  如果数据类型为 **String**，则选择 **“启用拼写检查器”** 可在填充域时对所有字符串值运行拼写检查器。  
  
8.  如果数据类型为 **String**，则选择 **“禁用语法错误算法”** 可填充域而不会检查字符串值是否存在语法错误。  
  
9. 单击“确定” 。  
  
10. 单击 **“完成”** 以完成域管理活动，如 [结束域管理活动](../../2014/data-quality-services/end-the-domain-management-activity.md)中所述。  
  
##  <a name="FollowUp"></a> 跟进：创建域后  
 在创建域后，您可以对域执行其他域管理任务，可以执行知识发现以便向域添加知识，或者可以向域添加匹配策略。 有关详细信息，请参阅[执行知识发现](../../2014/data-quality-services/perform-knowledge-discovery.md)、[管理域](../../2014/data-quality-services/managing-a-domain.md)或[创建匹配策略](../../2014/data-quality-services/create-a-matching-policy.md)。  
  
  
