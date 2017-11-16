---
title: "在知识发现中从 Excel 文件中导入域 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4d3a3940-6c2a-4dc4-90eb-86f26012c165
caps.latest.revision: "24"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f70a64af56ba104060d3cea8d4ad55a50d02cc9e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="import-domains-from-an-excel-file-in-knowledge-discovery"></a>在知识发现中从 Excel 文件中导入域
  本主题介绍如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 知识发现活动中从某一 Excel 文件导入一个或多个域。 该导入过程简化了知识生成过程，并且可以节省时间和精力。 借助这一方法，在 Excel 文件或文本文件中具有数据的人士能够创建包含这些数据的知识库。 （有关将值导入到现有知识库的域中的详细信息，请参阅[将值从 Excel 文件导入到域](../data-quality-services/import-values-from-an-excel-file-into-a-domain.md)。）不支持导出到 Excel 文件。  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Prerequisites"></a> 先决条件  
 若要从 Excel 文件导入域，Excel 必须安装在装有 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 的计算机上；您必须使用域值创建了一个 Excel 文件（请参阅 [How the import works](#How)）；并且必须创建并打开了要将域导入其中的知识库。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 权限  
 您必须具有针对 DQS_MAIN 数据库的 dqs_kb_editor 或 dqs_administrator 角色，才能从 Excel 文件导入域。  
  
##  <a name="Import"></a> 将域从 Excel 文件中导入到知识库中  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，执行以下操作之一：  
  
    -   通过以下方式创建要导入的新知识库：单击 **“新建知识库”**，为新知识库输入名称，为 **“创建知识库自”** 选择 **“无”**，选择 **“知识发现”** 活动，然后单击 **“创建”**。  
  
    -   通过以下方式打开要导入的现有知识库：单击 **“打开知识库”**，选择知识库，选择 **“知识发现”**，然后单击 **“下一步”**。  
  
3.  在“映射”  页中，为“数据源”  选择“Excel 文件” 。  
  
4.  在 **“Excel 文件”** 行中单击 **“浏览”** 。  
  
5.  在 **“选择 Excel 文件”** 对话框中，移到包含您要从其导入的 Excel 文件的文件夹，选择该 Excel 文件，然后单击 **“打开”**。  
  
6.  从 **“工作表”** 下拉列表中，选择您要从其导入的 Excel 文件中的工作表。  
  
7.  如果您希望第一行作为数据标头，并且希望第一行中的值用作列名称，则选择 **“将第一行用作标头”** 。 如果您希望第一行作为数据值，则取消选择 **“将第一行用作标头”** ，在此情况下，DQS 将使用 Excel 标头名称（字母）用于列。  
  
8.  选择某一列，然后或者将某个现有域映射到该列，或者创建一个新域，方法是单击 **“创建域”** 图标，在 **“创建域”** 对话框中创建一个域，然后将该域映射到该列。 该域的数据类型必须与该列的数据类型匹配。 为电子表格的所有列重复上述步骤。  
  
9. 单击“下一步” 。  
  
10. 在 **“发现”** 页中，单击 **“开始”** 以便分析 Excel 电子表格中的数据。  
  
    > [!NOTE]  
    >  如果在上载完数据前离开该页，则文件上载过程将终止。  
  
11. 验证分析已成功完成，然后单击 **“下一步”**。  
  
12. 在 **“管理域值”** 页中，验证在 **“域”** 列表中列出了正确的域并且在域表中输入了值。  
  
13. 单击 **“完成”**，然后单击 **“发布”** 以便发布知识库，或者单击 **“否”** 以便不发布。  
  
14. 验证知识库已发布，然后单击 **“确定”**。  
  
##  <a name="FollowUp"></a> 跟进：在从 Excel 文件导入域后  
 在从 Excel 文件导入域之后，您可以将知识添加到域中，或在清理或匹配项目中使用域，具体取决于域的内容。 有关详细信息，请参阅[执行知识发现](../data-quality-services/perform-knowledge-discovery.md)、[管理域](../data-quality-services/managing-a-domain.md)、[管理复合域](../data-quality-services/managing-a-composite-domain.md)、[创建匹配策略](../data-quality-services/create-a-matching-policy.md)、[数据清理](../data-quality-services/data-cleansing.md)或[数据匹配](../data-quality-services/data-matching.md)。  
  
##  <a name="How"></a> How the import works  
 在导入操作中，DQS 按如下所示解释 Excel 文件：  
  
-   列表示域  
  
-   行表示数据记录  
  
-   第一行或者表示域名，或者是第一个数据值或记录，视 **“将第一行用作标题”** 复选框的设置而定。  
  
 下列规则适用于导入操作：  
  
-   此操作将域值导入到知识库中。 它不导入域规则或匹配策略。  
  
-   该 Excel 文件可以具有扩展名 .xlsx、.xls 或 .csv。 Microsoft Excel 必须安装在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 计算机上，以便导入域值或整个域。 支持 Excel 版本 2003 和更高版本。 如果使用 64 位版本的 Excel，将仅支持 Excel 2003 文件；而不支持 Excel 2007 或 2010 文件。  
  
-   Excel 64 位安装不支持 .xlsx 类型的 Excel 文件。 如果您使用的是 64 位 Excel，将以 .xls 文件保存电子表格文件。  
  
-   在 .xlsx 和 .xls 文件中，列的数据类型由前八行中最主要的数据类型确定。 如果某一单元不符合该数据类型，将向它提供 null 值。  
  
-   在 .csv 文件中，数据类型由前八行中的主要数据类型确定。  
  
-   Excel 电子表格中不符合域规则的值将作为无效值导入。  
  
-   如果该 Excel 文件未采用正确的格式或已损坏，则导入操作将导致错误。  
  
  
