---
title: 更改默认 Reporting Services 传递扩展插件 | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- Report Manager [Reporting Services], default delivery extension
ms.assetid: 5f6fee72-01bf-4f6c-85d2-7863c46c136b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b5de95f97dc6ba0b8adb1cc0ad37f3ad08e59c1e
ms.sourcegitcommit: 9ece10c2970a4f0812647149d3de2c6b75713e14
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/16/2018
ms.locfileid: "51813090"
---
# <a name="change-the-default-reporting-services-delivery-extension"></a>更改默认 Reporting Services 传递扩展插件
  你可以通过修改 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 配置设置，来更改显示在订阅定义页的“传递方式”  列表中的默认传递扩展插件。 例如，你可以修改该配置，以便在用户创建新订阅时，文件共享传递（而非电子邮件传递）默认处于选中状态。 你还可以更改传递扩展插件在用户界面中的排列顺序。  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 本机模式 | [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 同时包含“电子邮件”和“Windows 文件共享”这两种传递扩展插件。 如果您部署了自定义扩展插件或第三方扩展插件来支持自定义传递，则报表服务器可能具有其他传递扩展插件。 传递扩展插件的可用性取决于它是否在报表服务器上进行了部署。  
  
## <a name="default-native-mode-report-server-configuration"></a>默认的本机模式报表服务器配置  
 报表管理器的“传递方式”  列表中传递扩展插件的显示顺序取决于 **RSReportServer.config** 文件中传递扩展插件项的顺序。 例如，下图显示列表中最先显示的是“电子邮件”，并且它默认处于选中状态。  
  
 ![传递扩展插件的默认列表](../../reporting-services/subscriptions/media/ssrs-default-delivery.png "default list of delivery extensions")  
  
 以下是 **RSReportServer.config** 的默认部分，用于控制默认传递扩展插件及其在报表管理器中的显示顺序。 请注意，“电子邮件”最先显示在该文件中，并且已设置为默认项。  
  
```  
<DeliveryUI>  
     <Extension Name="Report Server Email" Type="Microsoft.ReportingServices.EmailDeliveryProvider.EmailDeliveryProviderControl,ReportingServicesEmailDeliveryProvider">  
          <DefaultDeliveryExtension>True</DefaultDeliveryExtension>  
               <Configuration>  
               <RSEmailDPConfiguration>  
                    <DefaultRenderingExtension>MHTML</DefaultRenderingExtension>  
               </RSEmailDPConfiguration>  
               </Configuration>  
     </Extension>  
     <Extension Name="Report Server FileShare" Type="Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareUIControl,ReportingServicesFileShareDeliveryProvider"/>  
</DeliveryUI>  
```  
  
#### <a name="configure-file-share-delivery-as-the-default-delivery-extension-in-report-manager"></a>将“文件共享传递”配置为报表管理器中的默认传递扩展插件  
  
1.  此过程中的步骤可用于修改该配置，以便“文件共享传递”可作为第一个选项列在 UI 中，并默认处于选中状态。  
  
     在文本编辑器中打开 RSReportServer.config 文件。 有关配置文件的详细信息，请参阅 [RsReportServer.config Configuration File](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)。 更改该配置后，UI 的外观将类似于下图：  
  
     ![修改后的传递扩展插件的列表](../../reporting-services/subscriptions/media/ssrs-modified-delivery.png "modified list of delivery extensions")  
  
2.  将 DeliveryUI 部分修改为如以下示例所示，并注意关键更改：  
  
    1.  文件共享扩展插件位于电子邮件扩展插件之前。 这将更改这两种扩展插件在报表管理器中的排列顺序。  
  
    2.  文件共享扩展插件包含 DefaultExtension 标记 `<DefaultDeliveryExtension>True</DefaultDeliveryExtension>` ，以及已添加 `</Extension>`的扩展插件结束标记。  
  
    3.  电子邮件扩展插件不再配置为默认设置。 `<DefaultDeliveryExtension>False</DefaultDeliveryExtension>`  
  
    ```  
    <DeliveryUI>  
         <Extension Name="Report Server FileShare" Type="Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareUIControl,ReportingServicesFileShareDeliveryProvider">  
              <DefaultDeliveryExtension>True</DefaultDeliveryExtension>  
         </Extension>  
         <Extension Name="Report Server Email" Type="Microsoft.ReportingServices.EmailDeliveryProvider.EmailDeliveryProviderControl,ReportingServicesEmailDeliveryProvider">  
         <DefaultDeliveryExtension>False</DefaultDeliveryExtension>  
         <Configuration>  
              <RSEmailDPConfiguration>  
                   <DefaultRenderingExtension>MHTML</DefaultRenderingExtension>  
              </RSEmailDPConfiguration>  
         </Configuration>  
         </Extension>  
    </DeliveryUI>  
    ```  
  
3.  保存配置文件。  
  
4.  报表服务器将在几分钟内重新加载该配置文件，随后新设置将生效。 你可以重新启动报表服务器服务，以强制加载配置文件。  
  
     读取配置文件时，以下事件将被写入 Windows 事件日志中。  
  
     **事件 ID：** 109  
  
     **源：** 报表服务器 Windows 服务（实例名称）  
  
     已修改 RSReportServer.config 文件  
  
## <a name="sharepoint-mode-report-servers"></a>SharePoint 模式报表服务器  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 模式会将扩展插件信息存储在 SharePoint 服务应用程序数据库中，而非 RsrReportServer.config 文件中。 在 SharePoint 模式下，传递扩展插件配置将使用 PowerShell 进行修改。  
  
#### <a name="configure-the-default-delivery-extension"></a>配置默认传递扩展插件  
  
1.  打开“SharePoint Management Shell” 。  
  
2.  如果你已经知道 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序的名称，则可以跳过此步骤。 使用以下 PowerShell，将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序列在 SharePoint 场中。  
  
    ```  
    get-sprsserviceapplication | format-list *  
    ```  
  
3.  运行以下 PowerShell，以验证 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 服务应用程序“ssrsapp”的当前默认传递扩展插件。  
  
    ```  
    $app=get-sprsserviceapplication | where {$_.name -like "ssrsapp*"};Get-SPRSExtension -identity $app | where{$_.ServerDirectivesXML -like "<DefaultDelivery*"} | format-list *  
  
    ```
  
## <a name="see-also"></a>另请参阅  
 [RsReportServer.config 配置文件](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [RsReportServer.config Configuration File](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Reporting Services 中的文件共享传递](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md)   
 [Reporting Services 中的电子邮件传递](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md)   
 [针对电子邮件传递配置报表服务器（SSRS 配置管理器）](https://msdn.microsoft.com/b838f970-d11a-4239-b164-8d11f4581d83)  
  
<!-- TODO:
The above See Also link to the old MSDN at...
https://msdn.microsoft.com/b838f970-d11a-4239-b164-8d11f4581d83

...is redirected to the following Docs link, for SQL Server 2014...

https://docs.microsoft.com/sql/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager?view=sql-server-2014

...So if I was not presently resolving conflicts with public repo PR, related to private repo PR 7827,
the better fix would be to replace the whole MSDN link with the newer Docs link (to which the older MSDN link is redirected).
Maybe later someone can perform this replacement, and under docs/reporting-services/ there are multiple similar replacement opportunities.
GeneMi , 2018/10/25
-->
