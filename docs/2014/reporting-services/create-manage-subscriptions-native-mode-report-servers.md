---
title: 创建和管理本机模式报表服务器的订阅 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], managing
ms.assetid: 7f46cbdb-5102-4941-bca2-5e0ff9012c6b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f93148eed4b059a3c7f9a591b08b885c948ffd4c
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59953683"
---
# <a name="create-and-manage-subscriptions-for-native-mode-report-servers"></a>创建和管理本机模式报表服务器的订阅
  本节包含有关订阅处理、监管和控制的主题。 标准订阅和数据驱动订阅的订阅管理有所不同。 标准订阅通常由用户所有并由用户进行管理。 而数据驱动订阅通常由报表服务器管理员创建和维护。  
  
 默认情况下，订阅和传递功能处于启用状态（电子邮件传递需要进行配置才能使用）。 默认的传递扩展插件包括报表服务器电子邮件和文件共享传递。 除非您创建或安装了自定义传递扩展插件，否则，订阅只能在处于本机模式的报表服务器上使用这些分发方法。  
  
## <a name="permissions-for-subscribing-to-reports-on-a-native-mode-report-server"></a>在处于本机模式的报表服务器上订阅报表的权限  
 可以通过对不同角色启用或禁用订阅任务，向所选的用户组提供订阅功能，具体取决于您对角色的使用方式。 用户可以通过两个任务来使用订阅功能：  
  
-   通过“管理单独的订阅”任务，用户可以创建、修改和删除对特定报表的订阅。 在预定义的角色中，“浏览器”和“报表生成器”角色包括此任务。 包括此任务的角色分配只允许用户管理自己创建的那些订阅。  
  
-   通过“管理所有订阅”任务，用户可以访问和修改所有订阅。 此任务是创建数据驱动订阅所必需的。 在预定义的角色中，只有“内容管理员”角色包括此任务。  
  
## <a name="disabling-subscriptions"></a>禁用订阅  
 若要阻止用户创建订阅，请从该角色中清除“管理单独的订阅”任务。 删除此任务后，“订阅”页将不可用。 在报表管理器中，“我的订阅”页显示为空（不能将它删除），即便它以前包含订阅也是如此。 删除与订阅相关的任务会使用户无法创建和修改订阅，但这不会删除现有的订阅。 现有订阅将继续执行，直到被删除。 有关删除订阅的详细信息，请参阅[创建、 修改和删除标准订阅&#40;本机模式下的 Reporting Services&#41;](subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)。  
  
 若要禁用订阅处理的报表服务器上，可以设置`ScheduleEventsAndReportDeliveryEnabled`属性设置为`False`中**Reporting Services 的外围应用配置**facet 的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]基于策略的管理。 这样可防止运行所有的计划操作。 您不能只是在报表服务器上关闭订阅处理。  
  
 有关如何取消报表服务器处理订阅的说明，请参阅[管理运行中的进程](subscriptions/manage-a-running-process.md)。  
  
## <a name="disabling-delivery-extensions"></a>禁用传递扩展插件  
 对于有权创建对某个给定报表的订阅的任何用户，可以使用报表服务器上安装的所有传递扩展插件。 可以自动使用并配置下列传递扩展插件：  
  
-   Windows 文件共享  
  
-   SharePoint 库（只能从 SharePoint 站点使用，该站点与处于 SharePoint 集成模式的报表服务器集成在一起）  
  
 电子邮件传递必须进行配置才能使用。 如果未对它进行配置，它将不可用。 有关详细信息，请参阅[为电子邮件传递配置报表服务器&#40;SSRS 配置管理器&#41;](../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)。  
  
 如果要关闭特定的扩展插件，则可以在 RSReportServer.config 文件中删除与该扩展插件相对应的条目。 有关详细信息，请参阅[RSReportServer Configuration File](report-server/rsreportserver-config-configuration-file.md)并[为电子邮件传递配置报表服务器&#40;SSRS 配置管理器&#41;](../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)。  
  
 删除某个传递扩展插件后，该插件在报表管理器或 SharePoint 站点中将不再可用。 删除传递扩展插件可能会使订阅变为非活动状态。 在删除扩展插件之前，请确保删除这些订阅或者将它们配置为使用其他传递扩展插件。  
  
## <a name="in-this-section"></a>本节内容  
 [使用我的订阅](subscriptions/use-my-subscriptions-native-mode-report-server.md)  
 介绍如何使用“我的订阅”页管理所拥有的订阅。  
  
 [暂停报表和订阅处理](subscriptions/disable-or-pause-report-and-subscription-processing.md)  
 介绍暂停报表处理的各种方法，例如，使用角色分配或禁用报表服务器资源。  
  
 [控制报表分发](../../2014/reporting-services/control-report-distribution.md)  
 介绍可用于控制报表分发的配置设置和传递选项。  
  
 [监视 Reporting Services 订阅](subscriptions/monitor-reporting-services-subscriptions.md)  
 介绍如何确定订阅是成功还是失败以及报表更改对现有订阅的影响。  
  
## <a name="see-also"></a>请参阅  
 [创建、 修改和删除标准订阅&#40;Reporting Services 本机模式&#41;](subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)  
  
  
