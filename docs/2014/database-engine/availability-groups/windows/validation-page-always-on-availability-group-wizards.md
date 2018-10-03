---
title: 验证页 （AlwaysOn 可用性组向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.newagwizard.validation.f1
- sql12.swb.addreplicawizard.validation.f1
- sql12.swb.adddatabasewizard.validation.f1
helpviewer_keywords:
- ', listeners'
ms.assetid: c8971556-240c-491a-bc86-9cc72f71a3dd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6cf16c8afb363a1b7727b6da3a5f75bf966ab0d2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48152948"
---
# <a name="validation-page-alwayson-availability-group-wizards"></a>“验证”页（AlwaysOn 可用性组向导）
  本帮助主题介绍 **“验证”** 页中的选项。 本主题适用于 [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)]的 [!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)]、 [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] 和 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]。 使用此页可以验证您的环境是否支持您在向导前面的页面中做出的所有配置选择。  
  
##  <a name="PageOptions"></a> “验证”页选项  
 **可用性组验证的结果。**  
 此网格显示每个已完成的验证步骤的结果。 网格列如下所示：  
  
 **名称**  
 显示描述特定步骤的短语。  
  
 **结果**  
 显示以下超链接文本之一。 有关给定验证步骤的结果的详细信息，请单击该超链接。  
  
|结果|Description|  
|------------|-----------------|  
|**错误**|指示验证步骤失败。 单击该链接可以查看错误消息。|  
|**已跳过**|指示已通过该验证步骤，因为您所做的选择不需要验证。 单击该链接可以查看跳过某步骤的原因。|  
|**成功**|指示此验证步骤已成功完成。|  
|**警告**|指示可用性组配置可能存在问题。  单击该链接可以查看警告消息。|  
  
 **重新运行验证**  
 如果您在该向导之外针对验证错误做出了更改，则单击此选项可以重复执行验证步骤。  
  

  
##  <a name="RelatedTasks"></a> 相关任务  
  
-   [使用“新建可用性组”对话框 (SQL Server Management Studio)](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [使用“将副本添加到可用性组向导”(SQL Server Management Studio)](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [使用“将数据库添加到可用性组向导”(SQL Server Management Studio)](availability-group-add-database-to-group-wizard.md)  
  
 
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组概述&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
  
