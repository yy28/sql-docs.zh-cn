---
title: "Deploying a Delivery Extension |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- delivery extensions [Reporting Services], deploying
- Extension element
- deploying [Reporting Services], extensions
ms.assetid: 4436ce48-397d-42c7-9b5d-2a267e2a1b2c
caps.latest.revision: 45
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: d072577828375a08c133bb1a68d93e652e5cf168
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---
# <a name="deploying-a-delivery-extension"></a>部署传递扩展插件
  传递扩展插件以 XML 配置文件的形式提供其配置信息。 该 XML 文件符合为传递扩展插件定义的 XML 架构。 传递扩展插件提供用于设置和修改配置文件的基础结构。  
  
 如果替换或升级某一传递扩展插件，则引用该传递扩展插件的所有订阅仍保持有效。  
  
 你已经编写并编译后你[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]到的传递扩展插件[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]库，你必须复制到相应的目录的扩展，并将条目添加到相应[!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]配置文件以便报表服务器可以找到它。  
  
## <a name="configuration-file-extension-element"></a>配置文件扩展插件元素  
 你部署到报表服务器的传递扩展插件需要作为输入**扩展**配置文件中的元素。 用于报表服务器的配置文件是 RSReportServer.config。  
  
 下表描述的特性**扩展**传递扩展插件的元素。  
  
|Attribute|Description|  
|---------------|-----------------|  
|**名称**|扩展插件的唯一名称（例如，“Report Server E-Mail”用于电子邮件传递扩展插件，“Report Server FileShare”用于文件共享传递扩展插件）。 **Name** 属性的最大长度是 255 个字符。 该名称在配置文件的 **Extension** 元素内的所有条目中必须唯一。 如果存在重复的名称，则报表服务器返回错误。|  
|**类型**|以逗号分隔的列表，其中包含完全限定的命名空间以及程序集的名称。|  
|**Visible**|值为**false**指示的传递扩展插件应不会显示在用户界面。 如果未包含此属性，则默认值为 **true**。|  
  
 有关 RSReportServer.config 文件的详细信息，请参阅[Reporting Services Configuration Files](../../../reporting-services/report-server/reporting-services-configuration-files.md)。  
  
## <a name="deploying-the-extension-to-the-report-server"></a>将扩展插件部署到报表服务器  
 报表服务器使用传递扩展插件处理和传递通知或报表。 您应将传递扩展插件程序集作为专用程序集部署到报表服务器。 还需要在报表服务器配置文件 RSReportServer.config 中生成一个条目。  
  
#### <a name="to-deploy-a-deliver-extension-assembly-to-a-report-server"></a>将传递扩展插件程序集部署到报表服务器  
  
1.  将程序集从临时位置复制到您要在其上使用此传递扩展插件的报表服务器的 bin 目录中。 报表服务器 bin 目录的默认位置为 %ProgramFiles%\Microsoft SQL Server\MSRS13。\<InstanceName > services\reportserver\bin。  
  
    > [!IMPORTANT]  
    >  如果您在尝试覆盖现有传递扩展插件程序集，则必须首先停止报表服务器服务，然后复制更新的程序集。 在复制程序集后重新启动您的服务。  
  
2.  在复制程序集文件后，打开 RSReportServer.config 文件。 RSReportServer.config 文件位于 %ProgramFiles%\Microsoft SQL Server\MSRS13 中。\<InstanceName > \Reporting Services\ReportServer 目录。 还需要在配置文件中为传递扩展插件程序集文件生成一个条目。 你可以打开具有的配置文件[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]或诸如记事本之类的简单文本编辑器。  
  
3.  找到**传递**RSReportServer.config 文件中的元素。 应当在以下位置为新创建的传递扩展插件生成一个条目：  
  
    ```  
    <Extensions>  
       <Delivery>  
          <Your extension configuration information goes here>  
       </Delivery>  
    </Extensions>  
    ```  
  
4.  为您的传递扩展插件添加一个条目。 条目应包含**扩展**元素替换为值**名称**和**类型**，并可能如下所示：  
  
    ```  
    <Extension Name="My Delivery Extension Name" Type="CompanyName.ExtensionName.MyDeliveryExtensionClass, AssemblyName" />  
    ```  
  
     值**名称**是传递扩展插件的唯一名称。 值**类型**是以逗号分隔的列表，其中包括您实现的类的完全限定的命名空间的条目<xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension>接口，跟 （不包括.dll 文件扩展名） 程序集的名称。 默认情况下，传递扩展插件是可见的。 若要隐藏用户界面，例如 web 门户中，从扩展插件将添加**可见**属性设为**扩展**元素，并将其设置为**false**。  
  
5.  最后，为你授予的自定义程序集添加的代码组**FullTrust**传递扩展插件的权限。 通过将代码组添加到 rssrvpolicy.config 文件位于 %ProgramFiles%\Microsoft SQL Server\MSRS13 在默认情况下执行此操作。\<InstanceName > \Reporting Services\ReportServer。 代码组可能如下所示：  
  
    ```  
    <CodeGroup class="UnionCodeGroup"  
       version="1"  
       PermissionSetName="FullTrust"  
       Name="MyExtensionCodeGroup"  
       Description="Code group for my delivery extension">  
          <IMembershipCondition class="UrlMembershipCondition"  
             version="1"  
             Url="C:\Program Files\Microsoft SQL Server\MSRS13.<InstanceName>\Reporting Services\ReportServer\bin\MyExtensionAssembly.dll"  
           />  
    </CodeGroup>  
    ```  
  
     URL 成员身份仅是您可能为传递扩展插件选择的多个成员身份条件之一。 有关代码访问安全的详细信息[!INCLUDE[ssRS](../../../includes/ssrs-md.md)]，请参阅。[安全开发 &#40;Reporting Services &#41;](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md)  
   
## <a name="verifying-the-deployment"></a>验证部署  
 您可以使用 Web 服务 <xref:ReportService2010.ReportingService2010.ListExtensions%2A> 方法，验证是否已向报表服务器成功地部署了传递扩展插件。 你也可以打开 web 门户，并验证你的扩展包括在订阅可用的传递扩展插件的列表。 有关 web 门户和订阅的详细信息，请参阅[订阅和传递 &#40;Reporting Services &#41;](../../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md).  
  
## <a name="see-also"></a>另请参阅  
 [Implementing a Delivery Extension](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 扩展库](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

