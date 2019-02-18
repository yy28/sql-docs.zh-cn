---
title: 将知识库导出到 .dqs 文件 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: a324ead5-c8aa-4e26-abe3-ef415add00f8
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 04cc1acdc8e3cdec83545671736a452a2c176d3d
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56038758"
---
# <a name="export-a-knowledge-base-to-a-dqs-file"></a>将知识库导出到 .dqs 文件

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  本主题介绍如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中将整个知识库导出到 .dqs 数据文件。 您可以将域或整个知识库导出到数据文件。 有关导出域的信息，请参阅[将域导出到 .dqs 文件](../data-quality-services/export-a-domain-to-a-dqs-file.md)。  
  
 将知识库导出为 .dqs 文件，然后将其作为另一个知识库导入，可以简化知识生成过程、节省时间并提高效率。 这样，您就可以与他人共享知识库及其知识。 .dqs 文件将包含所有知识库信息，其中包括域和匹配策略，但附加的引用数据信息除外。 如果需要，则在导入 .dqs 文件之后，您必须再次将所需的域附加到相应的引用数据服务。 此时将同时导出知识库中的已发布和未发布的数据。  
  
 导出过程创建的 .dqs 数据文件已加密，所以无法查看内容。  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Prerequisites"></a> 先决条件  
 若要将知识库导出到 .dqs 数据文件，您必须已创建并打开了知识库。 您无需具有要导出到的 .dqs 文件，系统将为您创建一个。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 您必须对 DQS_MAIN 数据库具有 dqs_kb_editor 或 dqs_administrator 角色，才能将知识库导出到 .dqs 数据文件。  
  
##  <a name="Export"></a> 将知识库导出到.dqs 文件  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，在域管理活动中打开知识库。  
  
3.  在“域管理”页（选择了任一选项卡）中，单击域列表上方的 **“导出知识库数据”** 图标，然后单击 **“导出知识库”**。 或者，您还可以在 **“域”** 列表中右键单击，将鼠标指针悬停在 **“导出”** 之上，然后单击 **“导出知识库”**。  
  
4.  在“导出到数据文件”对话框中，转到要保存该文件的文件夹，命名该文件或保留知识库名称，将“DQS 数据文件 (\*.dqs)”保留为“另存为”类型，然后单击“保存”。  
  
5.  在 **“导出知识库”** 对话框中，验证状态行是否指示导出已完成。 单击“确定” 。  
  
##  <a name="FollowUp"></a> 跟进：将域导出到 .dqs 文件后  
 将知识库导出到 .dqs 文件后，您可以将知识库导入到同一个 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] （使用新名称）或导入到另一个 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]中。  
  
  
