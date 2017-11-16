---
title: "打开、解锁、重命名和删除数据质量项目 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.dqs.dqproject.opendqproject.f1
helpviewer_keywords:
- data quality project,delete
- data quality project,rename
- data quality project,unlock
- data quality project,open
ms.assetid: de8a2b04-4673-4beb-b4cf-96a28cdf3a93
caps.latest.revision: "9"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 00e34abfcc2162483023fd4eace52581c12a1e30
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="open-unlock-rename-and-delete-a-data-quality-project"></a>打开、解锁、重命名和删除数据质量项目
  本主题介绍如何使用 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 管理数据质量项目，如打开、解锁、重命名和删除数据质量项目。  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="LimitationsRestrictions"></a> 限制和局限  
  
-   您不能打开其他用户创建的锁定项目。  
  
-   您不能解锁、重命名或删除其他用户创建的数据质量项目。  
  
-   您不能删除锁定的数据质量项目。 您必须先对其解锁后才能删除。  
  
-   您只能解锁您创建的数据质量项目。  
  
###  <a name="Prerequisites"></a> 先决条件  
 您必须至少具有一个数据质量项目才能进行管理。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 权限  
 您必须对 DQS_MAIN 数据库具有 dqs_kb_editor 或 dqs_kb_operator 角色才能管理数据质量项目。  
  
##  <a name="Open"></a> 打开数据质量项目  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，单击 **“打开数据质量项目”**。 将出现 **“打开项目”** 屏幕。  
  
     或者，可以通过单击 **“最近的数据质量项目”** 区域下列出的数据质量项目来打开。  
  
3.  在 **“打开项目”** 屏幕中，单击以选择要打开的数据质量项目，然后单击 **“打开”**。  
  
4.  数据质量项目打开时的状态就是上次在其中关闭该项目的活动的状态。 数据质量项目具有以下状态：  
  
    -   对于 **“清理”** 活动，数据质量项目可具有以下状态： **“清理 - 映射”**、 **“清理 - 清理”**、 **“清理 – 管理和查看结果”**和 **“清理 – 导出”**。  
  
    -   对于 **“匹配”** 活动，数据质量项目可具有以下状态： **“匹配 - 映射”**、 **“匹配 - 匹配”**、 **“匹配 – 存活”**和 **“匹配 – 导出”**。  
  
##  <a name="Unlock"></a> 解锁数据质量项目  
 数据质量项目在创建时处于锁定状态，以防其他用户使用或修改。 在完成操作后，如果您希望其他用户使用您的数据质量项目，则必须对该数据质量项目解锁。 锁定的项目将显示一个锁符号。  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，单击 **“打开数据质量项目”**。 将出现 **“打开项目”** 屏幕。  
  
3.  在 **“打开项目”** 屏幕中，右键单击您创建的锁定数据质量项目，再单击快捷菜单中的 **“解锁”** 。 系统将为此项目显示一个绿色对钩标记，指示项目未锁定。  
  
##  <a name="Rename"></a> 重命名数据质量项目  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，单击 **“打开数据质量项目”**。 将出现 **“打开项目”** 屏幕。  
  
3.  在 **“打开项目”** 屏幕中，右键单击您创建的数据质量项目，再单击快捷菜单中的 **“重命名”** 。  
  
4.  在 **“名称”** 列中，数据质量项目名称将变为可编辑的。 键入新名称，然后按 Enter。  
  
##  <a name="Delete"></a> 删除数据质量项目  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，单击 **“打开数据质量项目”**。 将出现 **“打开项目”** 屏幕。  
  
3.  在 **“打开项目”** 屏幕中，右键单击您创建的未锁定的数据质量项目，再单击快捷菜单中的 **“删除”** 。  
  
4.  将显示一条确认消息。 单击 **“是”**。  
  
  
