---
title: 配置清理和匹配的阈值
description: 了解如何在 SQL Server Data Quality Services （DQS）中配置在计算机辅助清理和匹配活动期间使用的阈值。
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
ms.openlocfilehash: 4fcbc8e4e6d6a9c1df07d8e1b1aa68c08c162817
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/31/2019
ms.locfileid: "75557888"
---
# <a name="configure-threshold-values-for-cleansing-and-matching---data-quality-services-dqs"></a>配置清理和匹配的阈值-Data Quality Services （DQS）

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  本主题介绍如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中配置在计算机辅助清理和匹配活动中使用的阈值。  
  
##  <a name="BeforeYouBegin"></a>开始之前  
  
###  <a name="Security"></a>安全  
  
####  <a name="Permissions"></a>访问  
 您必须对 DQS_MAIN 数据库具有 dqs_administrator 角色才能配置这些阈值。  
  
##  <a name="Configure"></a>配置阈值  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，单击 **“配置”**。  
  
3.  接下来，单击 "**常规设置**" 选项卡。此选项卡允许您指定清理和匹配活动的阈值。  
  
4.  若要为清理活动指定阈值，请在 **“交互式清理”** 区域下的以下各框中指定适当的值：  
  
    -   **建议**的最低分数：在计算机辅助清理过程中，DQS 将用于建议替换值的最低分数或置信度级别。 以相应百分比值的小数表示形式输入一个值。 例如，对于 75% 键入 0.75。 该值应小于或等于在 **“用于自动更正的最低分数”** 框中指定的值。 默认值为 0.7。  
  
    -   **自动更正的最低分数**：在计算机辅助清理过程中，DQS 将用于自动更正值的最小分数或置信度级别。 以相应百分比值的小数表示形式输入一个值。 例如，对于 90% 输入 0.9。 默认值为 0.8。  
  
5.  若要为匹配活动指定阈值，请在 **“匹配”** 区域下的 **“最低记录分数”** 框中指定一个值。 此值表示一条记录要被视为另一条记录的匹配项的最低分数。 默认值为 80%。  
  
6.  单击 **“关闭”**。  
  
  
