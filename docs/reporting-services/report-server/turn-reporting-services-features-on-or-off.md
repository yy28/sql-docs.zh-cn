---
title: 打开或关闭 Reporting Services 功能 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-server
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, configuration
- security [Reporting Services], strategies
ms.assetid: b69db02a-43a7-4fdc-ad9b-438d817a7f83
caps.latest.revision: 10
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: edb78cc093837b8eb2beb1c3afc882a723e9a138
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33028524"
---
# <a name="turn-reporting-services-features-on-or-off"></a>打开或关闭 Reporting Services 功能
  您可以关闭不用作锁定策略一部分的报表服务器功能，以减小生产报表服务器的攻击面。 在大多数情况下，需要同时运行各种 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能才能使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中提供的所有功能。 但是根据所用的部署模型，您可以禁用不需要的功能。 例如，如果所有报表处理均已配置为预定操作，则可以只启用后台处理。 同样，如果您只需要交互式的按需报表，则可以只运行报表服务器 Web 服务。  
  
 本主题中的过程将为您演示如何关闭本机模式 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 功能。 可以不同的方式配置这些功能，如直接编辑 `RsReportServer.config` 文件或使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中基于策略的管理的“Reporting Services 的外围应用配置”方面。 使用以下链接可以找到说明如何打开或关闭相应功能的步骤：  
  
-   [报表服务器 Web 服务](#RSWebSvc)  
  
-   [预定的事件和处理](#Sched)  
  
-   [Web 门户](#WebPortal)  
  
-   [报表生成器](#ReportBuilder)  
  
-   [报表数据源的 Windows 集成安全性](#WinIntSec)  
  
##  <a name="RSWebSvc"></a> Report Server Web Service  
  
#### <a name="to-turn-on-or-off-the-report-server-web-service-by-editing-configuration"></a>通过编辑配置打开或关闭报表服务器 Web 服务  
  
1.  在文本编辑器中打开 `RsReportServer.config` 文件。 有关详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的[修改 Reporting Services 配置文件 (RSreportserver.config)](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)。  
  
2.  若要打开报表服务器 Web 服务，请将 **IsWebServiceEnabled** 设置为 **true**：  
  
    ```  
    <IsWebServiceEnabled>true</IsWebServiceEnabled>  
    ```  
  
3.  若要关闭报表服务器 Web 服务，请将 **IsWebServiceEnabled** 设置为 **false**：  
  
    ```  
    <IsWebServiceEnabled>false</IsWebServiceEnabled>  
    ```  
  
4.  保存所做的更改，然后关闭该文件。  
  
#### <a name="to-turn-on-or-off-the-report-server-web-service-by-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 打开或关闭报表服务器 Web 服务  
  
1.  打开 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，然后连接到要配置的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 实例。  
  
2.  在“对象资源管理器”中右键单击 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 节点，指向“策略”，然后单击“方面”。  
  
3.  在 **“方面”** 列表中，选择 **Reporting Services 的外围应用配置器**。  
  
4.  在 **“方面属性”** 下：  
  
    -   若要打开报表服务器 Web 服务，请将 **WebServiceAndHTTPAccessEnabled** 设置为 **True**。  
  
    -   若要关闭报表服务器 Web 服务，请将 **WebServiceAndHTTPAccessEnabled** 设置为 **False**。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="Sched"></a> 预定的事件和传递  
  
#### <a name="to-turn-on-or-off-scheduled-events-and-delivery-by-editing-configuration"></a>通过编辑配置打开或关闭预定的事件和传递  
  
1.  在文本编辑器中打开 RsReportServer.config 文件。 有关详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的[修改 Reporting Services 配置文件 (RSreportserver.config)](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)。  
  
2.  若要打开预定的报表处理和传递，请将 **IsSchedulingService**、 **IsNotificationService**和 **IsEventService** 设置为 **true**：  
  
    ```  
    <IsSchedulingService>true</IsSchedulingService>  
    <IsNotificationService>true</IsNotificationService>  
    <IsEventService>true</IsEventService>  
    ```  
  
3.  若要关闭预定的报表处理和传递，请将 **IsSchedulingService**、 **IsNotificationService**和 **IsEventService** 设置为 **false**：  
  
    ```  
    <IsSchedulingService>false</IsSchedulingService>  
    <IsNotificationService>false</IsNotificationService>  
    <IsEventService>false</IsEventService>  
    ```  
  
4.  保存所做的更改，然后关闭该文件。  
  
> [!NOTE]  
>  不能完全关闭后台处理，因为它提供执行服务器操作所需的数据库维护功能。  
  
#### <a name="to-turn-on-or-off-scheduled-events-and-delivery-by-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 打开或关闭预定的事件和传递  
  
1.  打开 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，然后连接到要配置的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 实例。  
  
2.  在“对象资源管理器”中右键单击 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 节点，指向“策略”，然后单击“方面”。  
  
3.  在 **“方面”** 列表中，选择 **Reporting Services 的外围应用配置器**。  
  
4.  在 **“方面属性”** 下：  
  
    -   若要打开预定的事件和传递，请将 **ScheduleEventsAndReportDeliveryEnabled** 设置为 **True**。  
  
    -   若要关闭预定的事件和传递，请将 **ScheduleEventsAndReportDeliveryEnabled** 设置为 **False**。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
> [!NOTE]  
>  不能完全关闭后台处理，因为它提供执行服务器操作所需的数据库维护功能。  
  
##  <a name="WebPortal"></a>Web 门户
  
在以前版本中，可以通过将“IsReportManagerEnabled”设置为 false 来禁用报表管理器。 从 SQL Server 2016 Reporting Services 累积更新 2 开始已弃用“IsReportManagerEnabled”。 将始终启用 Web 门户。
  
##  <a name="ReportBuilder"></a> 报表生成器  
  
#### <a name="to-turn-on-or-off-report-builder-by-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 打开或关闭报表生成器  
  
1.  打开 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，然后连接到要配置的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 实例。  
  
2.  在对象资源管理器中右键单击 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 节点，然后单击“属性”。  
  
3.  在 **“服务器属性”** 对话框中，单击 **“选择页”** 下的 **“安全性”**。  
  
    -   若要打开报表生成器，请选择 **“启用特别报告执行”** 选项。  
  
    -   若要关闭报表生成器，请取消选择 **“启用特别报告执行”** 选项。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="WinIntSec"></a> Windows 集成安全性  
  
#### <a name="to-turn-on-or-off-windows-integrated-security-by-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 打开或关闭 Windows 集成安全性  
  
1.  打开 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，然后连接到要配置的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 实例。  
  
2.  在对象资源管理器中右键单击 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 节点，然后单击“属性”。  
  
3.  在 **“服务器属性”** 对话框中，单击 **“选择页”** 下的 **“安全性”**。  
  
    -   若要打开 Windows 集成安全性，请选择 **“对报表数据源启用 Windows 集成安全性”** 选项。  
  
    -   若要关闭 Windows 集成安全性，请取消选择 **“对报表数据源启用 Windows 集成安全性”** 选项。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 配置管理器（SSRS 本机模式）](http://msdn.microsoft.com/en-us/63519ef4-e68a-42fb-9cf7-31228ea4e434)  
 更多疑问？ [请访问 Reporting Services 论坛](http://go.microsoft.com/fwlink/?LinkId=620231)
  
  
