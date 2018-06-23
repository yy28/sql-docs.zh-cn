---
title: 配置清理和匹配活动的阈值 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dqs.admin.config.general.f1
helpviewer_keywords:
- cleansing,threshold value
- cleansing threshold values
- matching,threshold value
ms.assetid: d2305409-7115-45a4-8f60-1213c0a47368
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 19425baf1fcf1f3fef0a4cf630242d8b16a35f9e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36025244"
---
# <a name="configure-threshold-values-for-cleansing-and-matching"></a>配置清理和匹配活动的阈值
  本主题介绍如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中配置在计算机辅助清理和匹配活动中使用的阈值。  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 您必须对 DQS_MAIN 数据库具有 dqs_administrator 角色才能配置这些阈值。  
  
##  <a name="Configure"></a> 配置阈值  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][运行 Data Quality Client 应用程序](../../2014/data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 主屏幕中，单击 **“配置”**。  
  
3.  接下来，单击 **“常规设置”** 选项卡。通过此选项卡可以为清理活动以及匹配活动指定阈值。  
  
4.  若要为清理活动指定阈值，请在 **“交互式清理”** 区域下的以下各框中指定适当的值：  
  
    -   **用于建议的最低分数**：在计算机辅助清除过程中 DQS 用于建议替换值的最低分数或置信度。 以相应百分比值的小数表示形式输入一个值。 例如，对于 75% 键入 0.75。 该值应小于或等于在 **“用于自动更正的最低分数”** 框中指定的值。 默认值为 0.7。  
  
    -   **用于自动更正的最低分数**：在计算机辅助清理过程中 DQS 用于自动更正值的最低分数或置信度。 以相应百分比值的小数表示形式输入一个值。 例如，对于 90% 输入 0.9。 默认值为 0.8。  
  
5.  若要为匹配活动指定阈值，请在 **“匹配”** 区域下的 **“最低记录分数”** 框中指定一个值。 此值表示一条记录要被视为另一条记录的匹配项的最低分数。 默认值为 80%。  
  
6.  单击 **“关闭”**。  
  
  