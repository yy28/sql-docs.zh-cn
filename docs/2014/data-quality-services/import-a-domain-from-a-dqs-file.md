---
title: 从 .dqs 文件导入域 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: fabd88b0-22b3-4543-a993-6d5b202ded80
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: c22babc0f8a4ff56ef845ca0fc0b5cd2b31475e1
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56011469"
---
# <a name="import-a-domain-from-a-dqs-file"></a>从 .dqs 文件导入域
  本主题说明如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中将域从 .dqs 文件导入到现有知识库。 通过从 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 应用程序导出域或知识库可创建 .dqs 数据文件。 .dqs 数据文件已加密，因此无法查看。  
  
 通过使用 .dqs 数据文件从一个知识库中导出域，然后将域导入到另一个知识库，可以简化知识生成过程、节省时间并提高效率。 这样，您就可以与他人共享域及其知识，同时节省时间。 您可以导入一个单一域或一个复合域（包含多个单一域）。 包含单一域的 .dqs 文件包含所有域数据，其中包括域属性、值和规则数据，但映射的引用数据信息除外。 包含复合域的 .dqs 文件包含所有复合域数据，其中包含复合域中包含的各单一域的所有域数据，以及复合域属性、值关系和 CD 规则，但映射的引用数据除外。 将导入已发布和未发布的数据。  
  
 在导入域时，域名称仍保持与最初导出的域的名称相同，除非域名称已经存在，在此情况下 DQS 将在此名称之后追加“_1”。 如果导入的复合域包含与现有域同名的单个域，则上述命名规则也适用。  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Prerequisites"></a> 先决条件  
 若要从 .dqs 文件导入域，必须已将一个单一域或一个复合域（包含多个单一域）导出到 .dqs 文件。 .dqs 文件必须只包含一个域。 您还必须已创建并打开了要将域导入到其中的知识库。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 您必须具有 DQS_MAIN 数据库的 dqs_kb_editor 或 dqs_administrator 角色，才能从 .dqs 数据文件导入域。  
  
##  <a name="Import"></a> Import a domain from a .dqs file  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../../2014/data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，在域管理活动中打开知识库。  
  
3.  单击 **“从数据文件导入域”** 图标。  
  
4.  在 **“从数据文件导入”** 对话框中，转到要从中导入文件的文件夹，选中该文件（DQS 文件类型），然后单击 **“打开”**。  
  
5.  在 **“导入域”** 对话框中，单击 **“确定”**。  
  
    > [!NOTE]  
    >  仅当您要从中导入的 .dqs 文件仅包含一个单一域或一个复合域（包含多个单个域）时，导入操作才会成功。  
  
6.  确认您导入的域显示在 **“域”** 列表中。 如果您导入复合域，请验证此复合域以及复合域中包含的单一域均出现在 **“域”** 列表中。  
  
##  <a name="FollowUp"></a> 跟进：从.dqs 文件导入域后  
 在从 .dqs 文件导入域之后，可以将知识添加到域中或在清理或匹配项目中使用域，具体取决于域的内容。 有关详细信息，请参阅[执行知识发现](../../2014/data-quality-services/perform-knowledge-discovery.md)、[管理域](../../2014/data-quality-services/managing-a-domain.md)、[管理复合域](../../2014/data-quality-services/managing-a-composite-domain.md)、[创建匹配策略](../../2014/data-quality-services/create-a-matching-policy.md)、[数据清理](../../2014/data-quality-services/data-cleansing.md)或[数据匹配](../../2014/data-quality-services/data-matching.md)。  
  
  
