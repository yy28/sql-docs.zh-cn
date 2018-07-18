---
title: 将域导出到 .dqs 文件 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: eba10d3d-b5c4-447b-8a30-fa07996cb28e
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e1bc39de73a6e5697c8ab2685b09c78188c36c27
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35310496"
---
# <a name="export-a-domain-to-a-dqs-file"></a>将域导出到 .dqs 文件

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  本主题介绍如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中将域导出到 .dqs 文件。 您可以将域或整个知识库导出到数据文件。 有关导出知识库的信息，请参阅[将知识库导出到 .dqs 文件](../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md)。  
  
 将域从一个知识库中导出到 .dqs 数据文件，然后将其导入到另一个知识库，可以简化知识生成过程、节省时间并提高效率。 这样，您就可以与他人共享域及其知识。  
  
 您可以导出单一域或复合域。 包含单一域的 .dqs 文件包含所有域数据，其中包括域属性、值和规则，但附加的引用数据信息除外。 包含复合域的 .dqs 文件包含所有复合域数据，其中包含复合域中包含的各域的所有域数据，以及复合域属性、关系和规则，但引用数据信息除外。 如果需要，则在导入 .dqs 文件之后，您必须再次将域或复合域附加到相应的引用数据服务。 将同时导出已发布和未发布的数据。  
  
 导出过程创建的 .dqs 数据文件已加密，所以无法查看内容。  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Prerequisites"></a> 先决条件  
 若要将域导出到 .dqs 数据文件，您必须已创建并选择了一个单一域或包含多个单一域的复合域。 您无需具有要导出到的 .dqs 文件，系统将为您创建一个。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 您必须对 DQS_MAIN 数据库具有 dqs_kb_editor 或 dqs_administrator 角色，才能将域导出到 .dqs 数据文件。  
  
##  <a name="Export"></a> Export a domain to a .dqs file  
 您可以从任何域管理页进行导出。 导出命令可通过用户界面中的控件和域列表窗格的上下文菜单中的命令来使用。  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，在域管理活动中打开知识库。  
  
3.  在 **“域管理”** 页（任意选项卡处于“选中”状态）中，在 **“域”** 列表中选择单一域或复合域。  
  
4.  单击域列表上方的 **“导出知识库数据”** 图标，然后单击 **“导出域”**。 或者，还可以在 **“域”** 列表中右键单击域，指向 **“导出”**，然后单击 **“导出域”**。  
  
5.  在“导出到数据文件”对话框中，转到要保存该文件的文件夹，命名该文件或保留默认名称，将“DQS 数据文件 (\*.dqs)”保留为“另存为”类型，然后单击“保存”。  
  
6.  在 **“导出域”** 对话框中，验证该对话框中的状态行是否指示导出已完成。 单击“确定” 。  
  
##  <a name="FollowUp"></a> 跟进：将域导出到 .dqs 文件后  
 将域导出到 .dqs 文件后，您可以将该域导入到另一个知识库。  
  
  
