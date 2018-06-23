---
title: 设置处理选项 (Reporting Services SharePoint 集成模式下) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SharePoint integration [Reporting Services], content management
- snapshots [Reporting Services], creating
ms.assetid: 453b19a1-739a-4b67-aeea-2069b52204e1
caps.latest.revision: 14
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 0b1d308718d1bfd1b9215cfe9595439f5657b95e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015176"
---
# <a name="set-processing-options-reporting-services-in-sharepoint-integrated-mode"></a>设置处理选项（SharePoint 集成模式下的 Reporting Services）
  可以对 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 报表设置处理选项，以决定何时进行数据处理。 还可以为报表处理设置超时值和用于决定是否为当前报表启用报表历史记录的选项。  
  
-   您可以按报表快照形式运行报表，以防止报表在任意时间运行（例如，在执行计划备份期间）。 报表快照通常按计划创建并在随后进行刷新，因此您可以精确地设定进行报表和数据处理的时间。 如果报表所基于的查询需要很长的运行时间，或查询使用的数据来自您需要在特定时间无人访问的数据源，则应以快照形式运行报表。  
  
-   报表服务器可以缓存已处理报表的副本，并在用户打开此报表时返回该副本。 缓存是一种性能增强技术。 在报表很大或需要频繁访问的情况下，缓存报表可以缩短检索该报表所需的时间。  
  
-   报表历史记录是以前运行的报表副本的集合。 您可以使用报表历史记录来维护一段时间以来的报表记录。 报表历史记录不适用于包含机密数据或个人数据的报表。 因此，报表历史记录只能包含使用单组特定凭据查询数据源的报表。此类凭据可以是已存储的凭据，也可以是在无人参与的情况下执行报表所用的凭据，并且对运行报表的所有用户都可用。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 与 SharePoint 的集成使用 SharePoint 的签出和签入内容管理功能将更新保存到 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 内容类型。 这包括创建报表快照。 因此，如果您在文档库上启用了版本控制，则当创建新的报表历史记录快照时，您将看到更新后的报表版本。 这是更新快照的副作用。 当更新快照时，它导致报表的 LastExecution 属性发生变化，而这会导致报表的版本发生变化。  
  
-   可以通过指定超时值来限制使用系统资源的方式。  
  
||  
|-|  
|**[!INCLUDE[applies](../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 模式|  
  
 **本主题内容：**  
  
-   [设置数据刷新选项](#bkmk_set_data_refresh)  
  
-   [设置报表缓存选项](#bkmk_set_report_caching)  
  
-   [设置处理超时值](#bkmk_set_processing)  
  
-   [设置报表历史记录选项和限制值](#bkmk_set_report_history)  
  
-   [设置数据库超时](#bkmk_set_database_timeout)  
  
##  <a name="bkmk_set_data_refresh"></a> 设置数据刷新选项  
  
1.  指向库中的报表。  
  
2.  单击向下箭头，然后选择 **“管理处理选项”**。  
  
3.  在 **“数据刷新选项”** 中，单击 **“使用快照数据”**。 如果看到“此报表无法通过快照运行，因为一个或多个数据源凭据未存储”这一信息，则表明报表未配置为以无人参与的方式运行，在设置此选项之前，必须将数据源修改为使用已存储凭据。  
  
4.  在 **“数据快照选项”** 中，选择 **“计划数据处理”**。  
  
5.  如果有要使用的现有共享计划，请选择 **“根据共享计划”** ，否则请单击 **“根据自定义计划”**，然后单击 **“配置”**。  
  
6.  选择频率、计划以及开始和结束日期，然后单击 **“确定”**。  
  
7.  如果想要立刻创建用于报表的快照数据而不等待预定的数据处理开始执行，则应在 **“数据快照选项”** 中选择 **“保存此页时创建或更新快照”** 。  
  
##  <a name="bkmk_set_report_caching"></a> 设置报表缓存选项  
  
1.  指向库中的报表。  
  
2.  单击向下箭头，然后选择 **“管理处理选项”**。  
  
3.  在 **“数据刷新选项”** 中，单击 **“使用缓存数据”**。 如果看到“此报表无法缓存，因为未存储一个或多个数据源凭据”这一信息，则表明报表未配置为以无人参与的方式运行，在设置此选项之前，必须将数据源修改为使用已存储凭据。  
  
4.  在 **“缓存选项”** 中，指定缓存的过期方式：  
  
    -   输入缓存将在其后过期的分钟数。  
  
    -   使用共享计划，在计划中指定的时间清除缓存。  
  
    -   创建自定义计划，在指定的时间清除缓存。  
  
##  <a name="bkmk_set_processing"></a> 设置处理超时值  
  
1.  指向库中的报表。  
  
2.  单击向下箭头，然后选择 **“管理处理选项”**。  
  
3.  如果要使用在报表服务器级指定的值，请在“处理超时”中选择“使用站点默认设置”。 如果要用无超时或不同的超时值来替代该值，请选择“不对报表处理时间设置超时”或“限制报表处理时间(秒)”。  
  
##  <a name="bkmk_set_report_history"></a> 设置报表历史记录选项和限制值  
  
1.  指向库中的报表。  
  
2.  单击向下箭头，然后选择 **“管理处理选项”**。  
  
3.  在 **“历史记录快照选项”** 中，指定数据处理的方式和时间，以及对数据处理进行保存的方式和时间。  
  
4.  在 **“历史记录快照限制”** 中，如果要使用在报表服务器级指定的值，请选择 **“使用站点默认设置”** 。 否则，请选择 **“不限制快照数”** 或 **“将快照数限制在”** 以指定自定义值。  
  
##  <a name="bkmk_set_database_timeout"></a> 设置数据库超时  
  
1.  使用 Windows PowerShell 设置 SharePoint 报表服务器的数据库超时。 有关详细信息，请参阅"获取和设置报表服务应用程序数据库的属性"部分[Reporting Services SharePoint 模式的 PowerShell cmdlet](../../2014/reporting-services/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)。  
  
## <a name="see-also"></a>请参阅  
 [设置报表处理属性](report-server/set-report-processing-properties.md)   
 [缓存报表 (SSRS)](report-server/caching-reports-ssrs.md)   
 [为报表和共享数据集处理设置超时值&#40;SSRS&#41;](report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)  
  
  