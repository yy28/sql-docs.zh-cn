---
title: 管理 （打开、 解锁、 重命名，并删除） 数据质量项目 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.dqproject.opendqproject.f1
helpviewer_keywords:
- data quality project,delete
- data quality project,rename
- data quality project,unlock
- data quality project,open
ms.assetid: de8a2b04-4673-4beb-b4cf-96a28cdf3a93
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: c77d1924bde3611bff4cf0328a659b2fea2cae45
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62792348"
---
# <a name="manage-open-unlock-rename-and-delete-a-data-quality-project"></a>管理（打开、解锁、重命名和删除）数据质量项目
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
  
####  <a name="Permissions"></a> Permissions  
 您必须对 DQS_MAIN 数据库具有 dqs_kb_editor 或 dqs_kb_operator 角色才能管理数据质量项目。  
  
##  <a name="Open"></a> 打开数据质量项目  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../../2014/data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，单击 **“打开数据质量项目”**。 将出现 **“打开项目”** 屏幕。  
  
     或者，可以通过单击 **“最近的数据质量项目”** 区域下列出的数据质量项目来打开。  
  
3.  在 **“打开项目”** 屏幕中，单击以选择要打开的数据质量项目，然后单击 **“打开”**。  
  
4.  数据质量项目打开时的状态就是上次在其中关闭该项目的活动的状态。 数据质量项目具有以下状态：  
  
    -   对于“清理”活动，数据质量项目可具有以下状态：“清除 - 映射”、“清除 - 清理”、“清除 - 管理和查看结果”以及“清除 - 导出”。  
  
    -   对于“匹配”活动，数据质量项目可具有以下状态：“匹配 - 映射”、“匹配 - 匹配”、“匹配 - 存活”以及“匹配 - 导出”。  
  
##  <a name="Unlock"></a> 解锁数据质量项目  
 数据质量项目在创建时处于锁定状态，以防其他用户使用或修改。 在完成操作后，如果您希望其他用户使用您的数据质量项目，则必须对该数据质量项目解锁。 锁定的项目将显示一个锁符号。  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../../2014/data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，单击 **“打开数据质量项目”**。 将出现 **“打开项目”** 屏幕。  
  
3.  在 **“打开项目”** 屏幕中，右键单击您创建的锁定数据质量项目，再单击快捷菜单中的 **“解锁”** 。 系统将为此项目显示一个绿色对钩标记，指示项目未锁定。  
  
##  <a name="Rename"></a> 重命名数据质量项目  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../../2014/data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，单击 **“打开数据质量项目”**。 将出现 **“打开项目”** 屏幕。  
  
3.  在 **“打开项目”** 屏幕中，右键单击您创建的数据质量项目，再单击快捷菜单中的 **“重命名”** 。  
  
4.  在 **“名称”** 列中，数据质量项目名称将变为可编辑的。 键入新名称，然后按 Enter。  
  
##  <a name="Delete"></a> 删除数据质量项目  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../../2014/data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，单击 **“打开数据质量项目”**。 将出现 **“打开项目”** 屏幕。  
  
3.  在 **“打开项目”** 屏幕中，右键单击您创建的未锁定的数据质量项目，再单击快捷菜单中的 **“删除”** 。  
  
4.  将显示一条确认消息。 单击 **“是”**。  
  
  
