---
title: 部署传递扩展插件 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- delivery extensions [Reporting Services], deploying
- Extension element
- deploying [Reporting Services], extensions
ms.assetid: 4436ce48-397d-42c7-9b5d-2a267e2a1b2c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3b95fbb99affb91743d5b922f748cae5554736f0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63164412"
---
# <a name="deploying-a-delivery-extension"></a>部署传递扩展插件
  传递扩展插件以 XML 配置文件的形式提供其配置信息。 该 XML 文件符合为传递扩展插件定义的 XML 架构。 传递扩展插件提供用于设置和修改配置文件的基础结构。  
  
 如果替换或升级某一传递扩展插件，则引用该传递扩展插件的所有订阅仍保持有效。  
  
 在将[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]传递扩展插件写入和编译到[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]库中后，必须将该扩展插件复制到相应的目录，并向相应[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]的配置文件添加一个条目，以便 Report Server 可以找到它。  
  
## <a name="configuration-file-extension-element"></a>配置文件扩展插件元素  
 您部署到报表服务器的传递扩展插件需要作为配置文件中的 `Extension` 元素输入。 用于报表服务器的配置文件是 RSReportServer.config。  
  
 下表介绍传递扩展插件的 `Extension` 元素的属性。  
  
|Attribute|说明|  
|---------------|-----------------|  
|`Name`|扩展插件的唯一名称（例如，“Report Server E-Mail”用于电子邮件传递扩展插件，“Report Server FileShare”用于文件共享传递扩展插件）。 
  `Name` 属性的最大长度是 255 个字符。 该名称在配置文件的 `Extension` 元素内的所有条目中必须唯一。 如果存在重复的名称，则报表服务器返回错误。|  
|`Type`|以逗号分隔的列表，其中包含完全限定的命名空间以及程序集的名称。|  
|`Visible`|值为 `false` 指示在用户界面中将不显示传递扩展插件。 如果未包含此属性，则默认值为 `true`。|  
  
 有关 RSReportServer.config 文件的详细信息，请参阅 [Reporting Services 配置文件](../../report-server/reporting-services-configuration-files.md)。  
  
## <a name="deploying-the-extension-to-the-report-server"></a>将扩展插件部署到报表服务器  
 报表服务器使用传递扩展插件处理和传递通知或报表。 您应将传递扩展插件程序集作为专用程序集部署到报表服务器。 还需要在报表服务器配置文件 RSReportServer.config 中生成一个条目。  
  
#### <a name="to-deploy-a-deliver-extension-assembly-to-a-report-server"></a>将传递扩展插件程序集部署到报表服务器  
  
1.  将程序集从临时位置复制到您要在其上使用此传递扩展插件的报表服务器的 bin 目录中。 Report Server bin 目录的默认位置为 "%ProgramFiles%\Microsoft SQL Server \ MSRS10_50"。\<InstanceName> \reporting services\reportserver\bin。  
  
    > [!IMPORTANT]  
    >  如果您在尝试覆盖现有传递扩展插件程序集，则必须首先停止报表服务器服务，然后复制更新的程序集。 在复制程序集后重新启动您的服务。  
  
2.  在复制程序集文件后，打开 RSReportServer.config 文件。 Rsreportserver.config 文件位于%ProgramFiles%\Microsoft SQL Server \ MSRS10_50 中。\<InstanceName> \reporting Services\ReportServer 目录。 还需要在配置文件中为传递扩展插件程序集文件生成一个条目。 您可以使用[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]或简单的文本编辑器（如记事本）打开该配置文件。  
  
3.  在 RSReportServer.config 文件中找到 `Delivery` 元素。 应当在以下位置为新创建的传递扩展插件生成一个条目：  
  
    ```  
    <Extensions>  
       <Delivery>  
          <Your extension configuration information goes here>  
       </Delivery>  
    </Extensions>  
    ```  
  
4.  为您的传递扩展插件添加一个条目。 您的条目应包括具有用于 `Extension` 和 `Name` 的值的 `Type` 元素，如下所示：  
  
    ```  
    <Extension Name="My Delivery Extension Name" Type="CompanyName.ExtensionName.MyDeliveryExtensionClass, AssemblyName" />  
    ```  
  
     
  `Name` 的值是传递扩展插件的唯一名称。 
  `Type` 的值是逗号分隔的列表，包括实现 <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension> 接口的类的完全限定命名空间的条目，后随程序集的名称（不包括 .dll 文件扩展名）。 默认情况下，传递扩展插件是可见的。 若要在用户界面（如报表管理器）中隐藏扩展插件，请将 `Visible` 属性添加到 `Extension` 元素，并将其设置为 `false`。  
  
5.  最后，为您的自定义程序集添加一个代码组，以便为您的传递扩展插件授予 `FullTrust` 权限。 为此，需要将代码组添加到默认位于%ProgramFiles%\Microsoft SQL Server \ MSRS10_50 中的 rssrvpolicy.config 文件。\<InstanceName> \reporting services\reportserver。 代码组可能如下所示：  
  
    ```  
    <CodeGroup class="UnionCodeGroup"  
       version="1"  
       PermissionSetName="FullTrust"  
       Name="MyExtensionCodeGroup"  
       Description="Code group for my delivery extension">  
          <IMembershipCondition class="UrlMembershipCondition"  
             version="1"  
             Url="C:\Program Files\Microsoft SQL Server\MSRS10_50.<InstanceName>\Reporting Services\ReportServer\bin\MyExtensionAssembly.dll"  
           />  
    </CodeGroup>  
    ```  
  
     URL 成员身份仅是您可能为传递扩展插件选择的多个成员身份条件之一。 有关 [!INCLUDE[ssRS](../../../includes/ssrs.md)] 中的代码访问安全性的详细信息，请参阅[安全开发 (Reporting Services)](../secure-development/secure-development-reporting-services.md)  
  
## <a name="deploying-the-extension-to-report-manager"></a>将扩展插件部署到报表管理器  
 如果您的传递扩展插件实现 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 接口，则该传递扩展插件可用于报表管理器订阅页。 为了使该订阅用户界面可用，需要将扩展插件部署到报表管理器。  
  
#### <a name="to-deploy-a-deliver-extension-assembly-to-report-manager"></a>将传递扩展插件程序集部署到报表管理器  
  
1.  将程序集从临时位置复制到报表管理器的 bin 目录中。 报表管理器 bin 目录的默认位置为 "%ProgramFiles%\Microsoft SQL Server \ MSRS10_50"。\<InstanceName> \reporting services\reportmanager\bin。  
  
2.  在复制程序集文件后，打开 RSReportServer.config 文件。 Rsreportserver.config 文件位于%ProgramFiles%\Microsoft SQL Server \ MSRS10_50 中。\<InstanceName> \reporting Services\ReportServer 目录。 还需要在配置文件中为传递扩展插件程序集文件生成一个条目。 您可以使用 Visual Studio .NET 或诸如记事本之类的简单文本编辑器打开此配置文件。  
  
3.  在 RSReportServer.config 文件中找到 `DeliveryUI` 元素。 应当在以下位置为新创建的传递扩展插件生成一个条目：  
  
    ```  
    <Extensions>  
       <DeliveryUI>  
          <Your extension configuration information goes here>  
       </DeliveryUI>  
    </Extensions>  
    ```  
  
4.  为您的传递扩展插件添加一个条目。 条目应包括具有 `Extension` 和 `Name` 的值的 `Type` 元素，可能类似如下所示：  
  
    ```  
    <Extension Name="My Delivery Extension Name" Type="CompanyName.ExtensionName.MyDeliveryUIExtensionClass, AssemblyName" />  
    ```  
  
     
  `Name` 的值是传递扩展插件的唯一名称。 
  `Type` 的值是逗号分隔的列表，包括实现 <xref:Microsoft.ReportingServices.Interfaces.ISubscriptionBaseUIUserControl> 接口的类的完全限定命名空间的条目，后随程序集的名称（不包括 .dll 文件扩展名）。  
  
    > [!IMPORTANT]  
    >  对于报表服务器和报表管理器配置文件条目，`Name` 属性的值必须相同。 如果它们不同，则您的服务器配置将无效。  
  
     最后，为您的自定义程序集添加一个代码组，以便为您的传递扩展插件授予 `FullTrust` 权限。 为此，需要将代码组添加到默认位于 C:\Program Files\Microsoft SQL Server \ MSRS10_50 中的 Rsmgrpolicy.config 文件。\<InstanceName> \reporting services\reportmanager。 代码组可能如下所示：  
  
    ```  
    <CodeGroup class="UnionCodeGroup"  
       version="1"  
       PermissionSetName="FullTrust"  
       Name="MyExtensionCodeGroup"  
       Description="Code group for my delivery UI extension">  
          <IMembershipCondition class="UrlMembershipCondition"  
             version="1"  
             Url="C:\Program Files\Microsoft SQL Server\MSRS10_50.<InstanceName>\Reporting Services\ReportManager\bin\MyExtensionAssembly.dll"  
           />  
    </CodeGroup>  
    ```  
  
     URL 成员身份仅是您可能为传递扩展插件选择的多个成员身份条件之一。 有关 [!INCLUDE[ssRS](../../../includes/ssrs.md)] 中的代码访问安全性的详细信息，请参阅[安全开发 (Reporting Services)](../secure-development/secure-development-reporting-services.md)  
  
## <a name="verifying-the-deployment"></a>验证部署  
 您可以使用 Web 服务 <xref:ReportService2010.ReportingService2010.ListExtensions%2A> 方法，验证是否已向报表服务器成功地部署了传递扩展插件。 还可以打开报表管理器，并验证您的扩展插件是否包括在用于订阅的可用传递扩展插件列表中。 有关报表管理器和订阅的详细信息，请参阅[订阅和传递 &#40;Reporting Services&#41;](../../subscriptions/subscriptions-and-delivery-reporting-services.md)。  
  
## <a name="see-also"></a>另请参阅  
 [实现传递扩展插件](implementing-a-delivery-extension.md)   
 [Reporting Services 扩展插件库](../reporting-services-extension-library.md)  
  
  
