---
title: 删除目录项 (Management Studio) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.deleteitems.f1
ms.assetid: b0599e01-6dc3-4484-80d4-022a412e0ebd
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b8576a1946368c7adc1a32aa66ce44e28603616a
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2019
ms.locfileid: "65573939"
---
# <a name="delete-catalog-items-management-studio"></a>删除目录项 (Management Studio)
  使用此页可以删除共享计划和角色定义。  
  
 如果删除由多个报表和订阅使用的共享计划，报表服务器将为以前使用该共享计划的每个报表和订阅都创建一个计划。 每个新计划都将包含已在共享计划中指定的日期、时间和重复执行模式。 请注意， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 不提供对于各个计划的集中管理。 如果删除共享计划，您现在将需要维护每一项的计划信息。 在删除共享计划之前，请使用 [“报表”页](../../reporting-services/tools/schedule-properties-reports-page.md) 确定当前哪些报表正在使用该共享计划。  
  
 对于角色定义，只能删除当前角色分配中未使用的角色定义。 如果您尝试删除当前正在使用的角色，则报表服务器将不删除该角色，您将看到有关该情况的错误消息。 如果此页只包含一个当前未使用的角色定义，则您单击 **“确定”** 时，该角色定义将被删除。 如果此页包含多个角色，您不能选择要保留或删除哪些角色。 当您单击 **“确定”** 时，将删除所有未使用的角色定义。  
  
 不能撤消删除操作。 若要恢复已删除的项，必须重新创建该项或还原报表服务器数据库的备份副本。  
  
## <a name="options"></a>选项  
 **名称**  
 指定要删除的项的名称。  
  
 **类型**  
 显示要删除的项的类型。  
  
 **所有者**  
 显示所有者的名称。 在大多数情况下，此名称为 System。  
  
 **“状态”**  
 显示删除操作的进度信息。  
  
 **错误**  
 如果在删除项的过程中出现错误，则显示错误代码。  
  
## <a name="see-also"></a>另请参阅  
 [删除项 (Management Studio)](../../reporting-services/tools/delete-an-item-management-studio.md)   
 [Management Studio 中报表服务器的 F1 帮助](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [创建、修改和删除计划](../../reporting-services/subscriptions/create-modify-and-delete-schedules.md)  
  
  
