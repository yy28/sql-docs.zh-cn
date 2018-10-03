---
title: 将值从 Excel 文件导入到域 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology:
- data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.kb.importfailing.f1
- sql13.dqs.kb.importselect.f1
- sql13.dqs.kb.failingvalues.f1
ms.assetid: 04cde693-2043-477f-8417-fcc463ca7195
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3fd18c3f8614a47a96f5a917fdeb6e59025a2590
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47828585"
---
# <a name="import-values-from-an-excel-file-into-a-domain"></a>将值从 Excel 文件导入到域

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  本主题介绍如何将值从 Excel 文件导入到 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 的域中。 使用 Excel 文件将域值导入到 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 应用程序中可以简化知识生成过程、节省时间并提高效率。 借助这一方法，在 Excel 文件或文本文件中具有有效数据值列表的人士能够将这些值导入到域中。 从 Excel 文件，您可以将域值导入到某个域中，或者将多个域导入到知识库中。 （有关将域导入到知识库的详细信息，请参阅[在知识发现中从 Excel 文件中导入域](../data-quality-services/import-domains-from-an-excel-file-in-knowledge-discovery.md)。）不支持导出到 Excel 文件。  
  
 您可以通过两种方式导入数据值：  
  
-   创建一个新域然后将值从 Excel 文件导入到该域中，在这种情况下，所有值都将添加到该域中。  
  
-   将值导入到一个现有的已填充域中，在这种情况下，仅导入新值。 将不会导入所有已存在的值。  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Prerequisites"></a> 先决条件  
 若要从 Excel 文件导入域，Excel 必须安装在装有 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 应用程序的计算机上，以便导入域值或整个域；您必须使用域值创建了一个 Excel 文件（请参阅 [How the import works](#How)）；并且必须创建并打开了要将域导入其中的知识库。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 您必须具有针对 DQS_MAIN 数据库的 dqs_kb_editor 或 dqs_administrator 角色，才能从 Excel 文件导入域值。  
  
##  <a name="Import"></a> Import values from an Excel file into a domain  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，在域管理活动中打开知识库。  
  
3.  如果将值添加到新域，则使用 **“创建域”** 图标创建一个新域，然后在域列表中选择这个新域。  
  
4.  如果将值添加到某个现有域中，则在域列表中选择该域。  
  
5.  单击 **“域值”** 选项卡，在图标栏中单击 **“导入值”** 图标，然后单击 **“从 Excel 导入有效值”**。  
  
6.  在 **“导入域值”** 对话框中，单击 **“浏览”**。  
  
7.  在 **“选择文件”** 对话框中，移到包含您要从其导入域值的 Excel 文件，选择该文件（具有 .xlsx、.xls 或 .csv 扩展名），然后单击 **“打开”**。 该文件必须或者位于您从其运行 DQS 的客户端上，或者位于用户有权访问的共享文件中。  
  
8.  从 **“工作表”** 下拉列表中，选择您要从其导入的工作表。  
  
9. 如果电子表格中的第一行表示域名，并且所有其他行表示有效的域值，则选择 **“将第一行用作标头”** 。  
  
10. 单击“确定” 。 将显示一个进度栏，指示成功导入了多少个值、未导入多少个值以及值的总数。 单击 **“取消”** 按钮将取消该过程。  
  
11. 确认“导入完成”显示在 **“导入域值”** 对话框中。 在此对话框中查看哪些值已成功导入、哪些值未导入。 该对话框将指示文件的名称和路径、操作的完成状态、成功导入了多少个值、未导入多少个值以及处理的值的总数。  
  
12. 对于未成功导入的那些值，单击 **“日志”** 可显示 **“导入域值 – 失败值”** 对话框，从而查看导入操作失败的原因。 **“失败值”** 列将显示未能从 Excel 文件导入到域中的值， **“原因”** 列将说明导入失败的原因。 单击 **“复制到剪贴板”** 可以将 **“失败值”** 表复制到剪贴板上，从而可以将该表复制到其他程序中，例如复制到 Excel 电子表格或记事本文件中。 单击 **“确定”** 关闭 **“失败值”** 对话框。  
  
13. 单击 **“确定”** 将完成导入操作并且关闭该对话框。 在导入成功完成后， **“域值”** 页上的域值列表将刷新并且将包含新导入的值。 筛选器将更改为 **“所有值”** ，并且 **“仅显示新内容”** 将被选中。 如果在导入操作后选中了 **“仅显示新内容”** ，将仅显示从 Excel 文件导入的值。  
  
14. 单击 **“完成”** 将值添加到知识库。  
  
##  <a name="FollowUp"></a> 跟进：在将值从 Excel 文件导入到域后  
 在将值导入到某个域中之后，您可以对该域执行其他域管理任务，可以执行知识发现以便向该域添加知识，或者可以向该域添加匹配策略。 有关详细信息，请参阅[执行知识发现](../data-quality-services/perform-knowledge-discovery.md)、[管理域](../data-quality-services/managing-a-domain.md)或[创建匹配策略](../data-quality-services/create-a-matching-policy.md)。  
  
##  <a name="Synonyms"></a> 导入同义词  
 按如下所示导入同义词：  
  
-   首先，导入所有值，然后建立同义词连接。  
  
-   如果无法连接同义词值，在日志屏幕将出现错误。 文件中的前导值和同义词可以导入到域中，但将不会被设为同义词。  
  
 以下内容适用于设置同义词连接的过程：  
  
-   如果该 Excel 文件中的前导值已在域中作为其他值的同义词存在，则您必须手动设置同义词（例如，在 Excel 文件中，我们希望值 A 将是值 B 的前导值，但在该域中，值 A 作为值 C 的同义词出现）。 除了在导入完成后手动设置同义词之外，您还可以取消现有同义词上的值的链接（例如，取消上面的值 A 和 C 的链接），然后导入文件。  
  
-   如果同义词已连接到其他前导值，则必须手动设置同义词。  
  
-   如果出于任何原因不能在应用程序中手动连接这些值，则这些值将不适用于导入操作。  
  
##  <a name="How"></a> How the import works  
 此操作将导入下列值：  
  
 在导入操作中，DQS 按如下所示从 Excel 文件进行导入：  
  
-   将导入正确的值和新值。 如果已经存在一个或多个导入的域值，这些值将不会导入。  
  
-   与域规则相矛盾的值将作为无效值导入。  
  
-   如果某个值不属于该域的数据类型或者为 null，将不会从文件中导入该值。  
  
-   值将按它们在文件中出现的顺序导入。  
  
-   每一行都表示某个域值。  
  
-   第一行或者表示域名，或者是第一个数据值或记录，视 **“将第一行用作标题”** 复选框的设置而定。 如果您在使用 .xslx 或 .xls 文件时选择了 **“将第一行用作标头”** ，则为 null 的任何列名都将自动转换为 F*n*，并且任何重复列都将在其名称后追加一个编号。  
  
-   如果您在导入操作完成前取消该操作，则该操作将回滚，并且将不会导入任何数据。  
  
-   第一列中的值将导入到域中。 如果除了第一列之外，还填充一个或多个其他列，则这些列中的值将作为同义词添加（请参阅 [导入同义词](#Synonyms)）。  
  
    -   预期的格式为：第一列将是前导值，第二列和以后的列将是同义词。  
  
    -   您可以在同一行或不同行中导入多个同义词。 例如，如果您要导入“NYC”和“New York City”作为“New York”的同义词，则可以导入在第 1 列中具有“New York”、在第 2 列中具有“NYC”、在第 3 列中具有“New York City”的单个行；或者，您可以导入在第 1 列中具有“New York”、在第 2 列中具有“NYC”的一行，以及在第一列中具有“New York”、在第 2 列中具有“New York City”的另一行。 请注意，如果值“New York”已在域中存在，将只添加同义词，并且用户在导入过程中将不会收到指示该值已存在的错误消息。 如果第一个值已不存在，则它将被添加到域中。  
  
 下列规则适用于要用于导入的 Excel 文件：  
  
-   该 Excel 文件可以具有扩展名 .xlsx、.xls 或 .csv。 Microsoft Excel 必须安装在装有 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 应用程序的计算机上，以便导入域值或整个域。 支持 Excel 版本 2003 和更高版本。 如果使用 64 位版本的 Excel，则仅支持 Excel 2003 文件；而不支持 Excel 2007 或 2010 文件。  
  
-   Excel 64 位安装不支持 .xlsx 类型的 Excel 文件。 如果您使用的是 64 位的 Excel，则将电子表格文件另存为 .xls 文件或 .csv 文件，或者改而安装 32 位的 Excel。  
  
-   在 .xlsx 和 .xls 文件中，列的数据类型由前八行确定。 如果前八行的列数据类型是混合类型，则列类型将是字符串。 如果第 9 行和更高行的单元不符合该数据类型，将向它提供 null 值。  
  
-   在 .csv 文件中，数据类型由前八行中的主要数据类型确定。  
  
-   如果该 Excel 文件未采用正确的格式或已损坏，则导入操作将导致错误。  
  
  
