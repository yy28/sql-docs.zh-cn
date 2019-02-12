---
title: 在 Data Quality Client 中打开 Integration Services 项目 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: a8bad2f1-8fb0-4d14-a978-11a5720e62d6
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 52a1bcb820d444e33ab034a09ee486592540e50c
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56020138"
---
# <a name="open-integration-services-projects-in-data-quality-client"></a>在数据质量客户端中打开 Integration Services 项目
  通过 [!INCLUDE[ssDQSCleansingLong](../includes/ssdqscleansinglong-md.md)] ，您可以在批处理模式下运行清理项目。 但是，有时您可能想要查看 Integration Services 包中的清理结果，这类似于您在 DQS 的数据质量项目中，在清理活动的 **“管理和查看结果”** 选项卡中查看清理结果。 通过 DQS，您可以在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 中打开 Integration Services 项目，就像从 **“打开项目”** 屏幕打开任何其他数据质量项目一样，并且您将具有在 Integration Services 项目中清理结果的交互式清理体验。  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="LimitationsRestrictions"></a> 限制和局限  
  
-   **的** “打开项目” [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]屏幕中仅提供已完成的 Integration Services 项目。 **“打开项目”** 屏幕中不提供失败或正在运行的项目。  
  
-   Integration Services 项目在**中打开时会进入交互式清理阶段（** “管理和查看结果” [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]选项卡）。 您无法进入 **“清理”** 或 **“映射”** 选项卡。 只能通过单击 **“下一步”** 转到 **“导出”** 选项卡。  
  
-   您无法从 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]中删除锁定的 Integration Services 项目。 您必须先对其解锁后才能删除。  
  
###  <a name="Prerequisites"></a> 先决条件  
 您必须成功完成运行包含某个包以及 DQS 清理组件的 Integration Services 项目，然后才能在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]中查看并打开该项目。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 您必须对 DQS_MAIN 数据库具有 dqs_kb_editor 或 dqs_kb_operator 角色，才能打开 Integration Services 项目。  
  
 ![使用顶部的链接的箭头图标](../2014-toc/media/uparrow16x16.gif "使用顶部的链接的箭头图标")[中此主题](#Intro)  
  
##  <a name="Open"></a> 打开 Integration Services 项目  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../../2014/data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，单击 **“打开数据质量项目”**。 将出现 **“打开项目”** 屏幕。  
  
3.  在 **“打开项目”** 屏幕上，可以通过以下方式之一标识 Integration Services 项目：  
  
    1.  **项目名称**：Integration Services 项目使用以下命名术语列出："Package.DQS Cleansing_*\<日期 > * *\<时间 >*_ {GUID}。" 每次成功地在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中运行同一个包，就会在“打开项目”屏幕中列出一个新项目。   
  
    2.  **项目类型**：在“打开项目”屏幕中，Integration Services 项目具有 SSIS 作为项目类型。  
  
     选择一个项目，然后单击 **“下一步”**。  
  
4.  Integration Services 项目将打开并进入交互式清理阶段（**“管理和查看结果”** 选项卡）。 您可以对 Integration Services 项目中的数据执行交互式清理。 有关“管理和查看结果”选项卡的详细信息，请参阅[使用 DQS（内部）知识清理数据](../../2014/data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)中的[交互式清理阶段](../../2014/data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Interactive)。  
  
5.  单击 **“下一步”** 以转到 **“导出”** 选项卡，您可以在此处将处理后的数据导出到以下任一位置：SQL Server 数据库中的新表、.csv 文件或 Excel 文件。 有关“导出”选项卡的详细信息，请参阅[使用 DQS（内部）知识清理数据](../../2014/data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)中的[导出阶段](../../2014/data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Export)  
  
6.  导出数据后，单击 **“完成”** 以关闭 Integration Services 项目。  
  
 ![使用顶部的链接的箭头图标](../2014-toc/media/uparrow16x16.gif "使用顶部的链接的箭头图标")[中此主题](#Intro)  
  
## <a name="see-also"></a>请参阅  
 [DQS 清理转换](../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)   
 [Integration Services (SSIS) 项目](../integration-services/integration-services-ssis-projects-and-solutions.md)  
  
  
