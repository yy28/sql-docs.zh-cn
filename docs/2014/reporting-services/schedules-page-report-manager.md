---
title: 计划页 （报表管理器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: ef19d96e-9f00-4434-950e-152dda9c1ced
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 927a9fc96e11bffdcacf7a12f09ee93d25f153fd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66102319"
---
# <a name="schedules-page-report-manager"></a>“计划”页（报表管理器）
  使用“计划”页可以创建、修改、删除、暂停或恢复共享计划。 共享计划是一个指定计划。您可以独立于报表、订阅以及其他需要计划信息的进程来创建和管理共享计划。 用户可以选择您提供的共享计划。  
  
 要删除、暂停或恢复共享计划，请选中您要修改的共享计划旁边的复选框。  
  
> [!NOTE]  
>  并非在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的每个版本中均提供此功能。 有关的各版本支持的功能列表[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，请参阅[SQL Server 2014 各个版本支持的功能](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
## <a name="navigation"></a>导航  
 使用以下过程导航到用户界面 (UI) 中的这一位置。  
  
### <a name="to-open-the-schedules-page"></a>打开“计划”页  
  
1.  打开报表管理器。  
  
2.  在页面顶部的右角，单击 **“站点设置”** 。 这会打开该站点的“常规属性”页。  
  
3.  选择 **“计划”** 选项卡。  
  
## <a name="options"></a>选项  
 **新建计划**  
 单击此选项可打开用于指定频率信息的“计划”页。  
  
 **删除**  
 单击此选项可删除共享计划。  
  
 **暂停**  
 单击此选项可暂时停止运行共享计划。 暂停计划将导致订阅和其他计划进程停止运行。  
  
 **恢复**  
 单击此选项可恢复已暂停的共享计划。 在暂停计划期间计划运行的进程将会失效，且不可恢复。  
  
 **“计划”**  
 显示当前定义的共享计划。 单击共享计划可以查看或编辑其频率信息。  
  
 **创建者**  
 显示创建共享计划的用户名。  
  
 **上次运行时间和下次运行**  
 显示共享计划的上次运行时间和下次运行时间。  
  
 **“状态”**  
 显示共享计划的状态是已暂停还是活动。  
  
## <a name="see-also"></a>请参阅  
 [创建、修改和删除计划](subscriptions/create-modify-and-delete-schedules.md)   
 [报表管理器的 F1 帮助](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
