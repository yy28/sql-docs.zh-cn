---
title: 设置报表处理属性 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- on-demand reports
- report processing [Reporting Services], execution properties
- snapshots [Reporting Services], running reports from
- cached reports [Reporting Services]
- report snapshots [Reporting Services], running reports from
- report execution snapshots [Reporting Services]
ms.assetid: b5cbc453-5986-423e-af44-1f243ef3edb1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4d4391fb3957c9b0d3529ebb51d038398786c15d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47838575"
---
# <a name="set-report-processing-properties"></a>设置报表处理属性
  报表执行属性控制报表的处理方式。 必须为每个报表分别设置执行属性。  
  
 若要设置报表执行属性，请在报表管理器中打开报表，再导航到“执行”属性页。 有关详细信息，请参阅[“处理选项”属性页（报表管理器）](http://msdn.microsoft.com/library/28f07c70-7132-4d15-9505-4fdf31dc9cc0)。 还可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 设置属性，请参阅[“处理选项”属性页（报表管理器）](http://msdn.microsoft.com/library/28f07c70-7132-4d15-9505-4fdf31dc9cc0)。  
  
## <a name="report-execution-modes"></a>报表执行模式  
 您既可以按需运行报表，也可以按快照形式运行报表。 以下部分介绍了各种运行方法。  
  
### <a name="running-reports-on-demand"></a>按需运行报表  
 您可以指定每次用户运行报表时，报表都查询数据源，这样，按需运行的报表将包含最新的数据。 对于每个打开或请求报表的用户，都会创建一个新报表实例；每个新实例都包含新查询的结果。 使用此方法时，如果有十个用户同时打开报表，则会向数据源发送十个要处理的查询。  
  
### <a name="running-reports-on-demand-from-cache"></a>通过缓存按需运行报表  
 为提高性能，您可以指定在用户运行报表时暂时缓存报表（和数据）。 如果随后有其他用户访问同一个报表，就可以向他们提供缓存的副本。 使用此方法时，如果有十个用户打开报表，则只有第一个请求会导致报表处理。 随后即会缓存报表，这样，其余九个用户将查看缓存的报表。  
  
 缓存的报表会按您指定的时间间隔从缓存中删除。 您可以指定时间间隔（分钟），也可以计划清空缓存的具体日期和时间。 有关详细信息，请参阅 [缓存报表 (SSRS)](../../reporting-services/report-server/caching-reports-ssrs.md)版本中预加载缓存的唯一方法。  
  
### <a name="running-reports-from-snapshots"></a>通过快照运行报表  
 报表快照是包含布局信息以及在特定时间点所检索到的数据的报表。 您可以按报表快照形式运行报表，以防止报表在任意时间运行（例如，在执行计划备份期间）。 报表快照通常按计划创建并在随后进行刷新，因此您可以精确地设定进行报表和数据处理的时间。 如果报表所基于的查询需要很长的运行时间，或查询使用的数据来自您需要在特定时间无人访问的数据源，则应以快照形式运行报表。  
  
 报表快照存储在报表服务器数据库中，随后当用户或进程（如订阅）请求报表时，即可从其中检索报表。 报表快照更新时，将用新的实例进行覆盖。 除非专门设置了相应选项以将报表快照添加到报表历史记录中，否则报表服务器不保存早期版本的报表快照。 有关详细信息，请参阅 [创建、修改和删除报表历史记录中的快照](../../reporting-services/report-server/create-modify-and-delete-snapshots-in-report-history.md)。  
  
 并非所有报表都可配置为以快照形式运行。 如果报表在获取报表数据时需要提示用户输入凭据，或使用 Windows 集成安全性，则无法为其创建快照。 如果希望以快照形式运行参数化报表，则必须在创建快照时指定要使用的默认参数。 与按需运行的报表不同，在打开报表后，就不可能为报表快照指定不同的参数值。 选择不同的参数值会引起新的报表处理请求，而这是不允许的。  
  
 在某些情况下，如果将按需运行报表配置为以快照形式运行，将会停用订阅。 对于将报表配置为按需运行时所定义的现有订阅，以下条件将导致报表服务器停用这些订阅：  
  
-   报表使用查询参数，而您选择特定的值作为默认参数，以满足以快照形式运行报表的要求。  
  
-   现有订阅配置使用的参数值与您为快照指定的默认参数值不同。  
  
 如果存在以上条件，则报表服务器将在订阅的下次计划运行时间禁用此订阅。 若要重新激活订阅，请打开订阅，再进行保存。 打开订阅后，报表服务器会将订阅参数值更新成为快照指定的参数值。 有关订阅的详细信息，请参阅[订阅和传递 (Reporting Services)](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)。  
  
## <a name="see-also"></a>另请参阅  
 [设置处理选项（SharePoint 集成模式下的 Reporting Services）](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)   
 [配置报表的执行属性（报表管理器）](../../reporting-services/reports/configure-execution-properties-for-a-report-report-manager.md)   
 [Reporting Services 概念 (SSRS)](../../reporting-services/reporting-services-concepts-ssrs.md)   
 [如何：向报表历史记录添加快照](../../reporting-services/report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [为报表数据源指定凭据和连接信息](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
  
