---
title: 打开、解锁、重命名和删除数据质量项目
description: 了解如何使用 SQL Server Data Quality Services 打开、解锁、重命名和删除数据质量项目。
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.dqproject.opendqproject.f1
helpviewer_keywords:
- data quality project,delete
- data quality project,rename
- data quality project,unlock
- data quality project,open
ms.assetid: de8a2b04-4673-4beb-b4cf-96a28cdf3a93
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 666e7fdbc080af3ed259dae978bd782e437eae2e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "75557798"
---
# <a name="open-unlock-rename-and-delete-a-data-quality-project---data-quality-services-dqs"></a>打开、解锁、重命名和删除数据质量项目-Data Quality Services （DQS）

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  本主题介绍如何使用 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 管理数据质量项目，如打开、解锁、重命名和删除数据质量项目。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> 限制和局限  
  
-   您不能打开其他用户创建的锁定项目。  
  
-   您不能解锁、重命名或删除其他用户创建的数据质量项目。  
  
-   您不能删除锁定的数据质量项目。 您必须先对其解锁后才能删除。  
  
-   您只能解锁您创建的数据质量项目。  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a>先决条件  
 您必须至少具有一个数据质量项目才能进行管理。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 您必须对 DQS_MAIN 数据库具有 dqs_kb_editor 或 dqs_kb_operator 角色才能管理数据质量项目。  
  
##  <a name="open-a-data-quality-project"></a><a name="Open"></a> 打开数据质量项目  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，单击 **“打开数据质量项目”**。 将出现 **“打开项目”** 屏幕。  
  
     或者，可以通过单击 **“最近的数据质量项目”** 区域下列出的数据质量项目来打开。  
  
3.  在 **“打开项目”** 屏幕中，单击以选择要打开的数据质量项目，然后单击 **“打开”**。  
  
4.  数据质量项目打开时的状态就是上次在其中关闭该项目的活动的状态。 数据质量项目具有以下状态：  
  
    -   对于 "**清理**" 活动，数据质量项目可具有以下状态： "**清理**"、"**清理-** 清理"、"**清理-管理和查看结果**" 和 "**清理导出**"。  
  
    -   对于“匹配”活动，数据质量项目可具有以下状态：“匹配 - 映射”、“匹配 - 匹配”、“匹配 - 存活”和“匹配 - 导出”********************。  
  
##  <a name="unlock-a-data-quality-project"></a><a name="Unlock"></a> 解锁数据质量项目  
 数据质量项目在创建时处于锁定状态，以防其他用户使用或修改。 在完成操作后，如果您希望其他用户使用您的数据质量项目，则必须对该数据质量项目解锁。 锁定的项目将显示一个锁符号。  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，单击 **“打开数据质量项目”**。 将出现 **“打开项目”** 屏幕。  
  
3.  在 **“打开项目”** 屏幕中，右键单击您创建的锁定数据质量项目，再单击快捷菜单中的 **“解锁”** 。 系统将为此项目显示一个绿色对钩标记，指示项目未锁定。  
  
##  <a name="rename-a-data-quality-project"></a><a name="Rename"></a> 重命名数据质量项目  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，单击 **“打开数据质量项目”**。 将出现 **“打开项目”** 屏幕。  
  
3.  在 **“打开项目”** 屏幕中，右键单击您创建的数据质量项目，再单击快捷菜单中的 **“重命名”** 。  
  
4.  在 **“名称”** 列中，数据质量项目名称将变为可编辑的。 键入新名称，然后按 Enter。  
  
##  <a name="delete-a-data-quality-project"></a><a name="Delete"></a> 删除数据质量项目  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，单击 **“打开数据质量项目”**。 将出现 **“打开项目”** 屏幕。  
  
3.  在 **“打开项目”** 屏幕中，右键单击您创建的未锁定的数据质量项目，再单击快捷菜单中的 **“删除”** 。  
  
4.  此时会显示确认消息。 单击 **“是”** 。  
  
  
