---
title: 配置清理和匹配的阈值
description: 了解如何在 SQL Server Data Quality Services （DQS）中配置在计算机辅助的清理和匹配活动期间使用的阈值。
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.admin.config.general.f1
helpviewer_keywords:
- cleansing,threshold value
- cleansing threshold values
- matching,threshold value
ms.assetid: d2305409-7115-45a4-8f60-1213c0a47368
author: swinarko
ms.author: sawinark
ms.openlocfilehash: cfb67f59d7a383d7ca7376c30435462c9a6199d7
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85814121"
---
# <a name="configure-threshold-values-for-cleansing-and-matching---data-quality-services-dqs"></a>配置清理和匹配的阈值-Data Quality Services （DQS）

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  本主题介绍如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中配置在计算机辅助清理和匹配活动中使用的阈值。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 权限  
 您必须对 DQS_MAIN 数据库具有 dqs_administrator 角色才能配置这些阈值。  
  
##  <a name="configuring-the-threshold-values"></a><a name="Configure"></a> 配置阈值  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，单击 **“配置”**。  
  
3.  接下来，单击 "**常规设置**" 选项卡。此选项卡允许您指定清理和匹配活动的阈值。  
  
4.  若要为清理活动指定阈值，请在 **“交互式清理”** 区域下的以下各框中指定适当的值：  
  
    -   **用于建议的最低分数**：在计算机辅助清除过程中 DQS 用于建议替换值的最低分数或置信度。 以相应百分比值的小数表示形式输入一个值。 例如，对于 75% 键入 0.75。 该值应小于或等于在 **“用于自动更正的最低分数”** 框中指定的值。 默认值为 0.7。  
  
    -   **用于自动更正的最低分数**：在计算机辅助清理过程中 DQS 用于自动更正值的最低分数或置信度。 以相应百分比值的小数表示形式输入一个值。 例如，对于 90% 输入 0.9。 默认值为 0.8。  
  
5.  若要为匹配活动指定阈值，请在 **“匹配”** 区域下的 **“最低记录分数”** 框中指定一个值。 此值表示一条记录要被视为另一条记录的匹配项的最低分数。 默认值为 80%。  
  
6.  单击“关闭”。  
  
  
