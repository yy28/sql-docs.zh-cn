---
title: "如何缓存一个报表 （报表管理器） |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- report execution properties [Reporting Services]
- cache [Reporting Services]
- cached reports [Reporting Services]
- schedules [Reporting Services], report expiration
- expiration [Reporting Services]
ms.assetid: 723d1cb0-c2e7-4763-8690-a6a7a8bbbb90
caps.latest.revision: 42
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: af00978c2afb28937a008f22eebe76f1a3f78eb1
ms.contentlocale: zh-cn
ms.lasthandoff: 06/13/2017

---
# <a name="cache-a-report-report-manager"></a>如何缓存一个报表（报表管理器）
  提高性能的一种方法是配置报表的缓存属性。 缓存报表后，会在一段时间内保存已呈现报表的副本。 请求该报表的第一个用户必须等到所有处理全部完成后才能查看报表。 以后在缓存期间请求该报表的用户可以立即查看它，因为处理已经完成。  
  
 可缓存的报表类型存在限制。 例如，如果报表输出随着用户标识的变化而变化，或者使用请求该报表的用户的安全令牌检索数据，则无法缓存此报表。 有关详细信息，请参阅 [缓存报表 (SSRS)](../../reporting-services/report-server/caching-reports-ssrs.md)。  
  
### <a name="to-schedule-the-expiration-of-a-cached-report"></a>计划缓存报表的过期时间  
  
1.  启动[报表管理器（SSRS 本机模式）](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)。  
  
2.  在报表管理器中，导航到 **“内容”** 页。 导航到要设置缓存属性的报表，悬停在该项上，然后单击下拉箭头。  
  
3.  在下拉菜单中，单击“管理”。  
  
4.  在左框架中，单击 **“处理选项”**。  
  
5.  在该页上，选择 **“始终用最新数据运行此报表”**。  
  
6.  选择以下两个缓存选项之一，并配置过期时间：  
  
    -   若要将缓存副本配置为在特定时间段后过期，请单击“缓存报表的临时副本。**在数分钟之后使报表副本过期**。 键入报表过期所需的分钟数。  
  
    -   若要将缓存副本配置为按计划过期，请单击“缓存报表的临时副本”。**按下列计划使报表副本过期。** 单击 **“配置”**，或选择一个共享计划以控制报表过期时间。  
  
7.  单击 **“应用”**。  
  
## <a name="see-also"></a>另请参阅  
 [设置报表处理属性](../../reporting-services/report-server/set-report-processing-properties.md)   
 [缓存报表 (SSRS)](../../reporting-services/report-server/caching-reports-ssrs.md)  
  
  
