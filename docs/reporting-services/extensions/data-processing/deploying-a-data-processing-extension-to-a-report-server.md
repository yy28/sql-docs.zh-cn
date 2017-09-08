---
title: "如何： 将数据处理扩展插件部署到报表服务器 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
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
- data processing extensions [Reporting Services], deploying
- assemblies [Reporting Services], data processing extension deployments
ms.assetid: e00dface-70f8-434b-9763-8ebee18737d2
caps.latest.revision: 45
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: a60c685ebdfd9d549e100cf5b5eda0ab056c1c46
ms.contentlocale: zh-cn
ms.lasthandoff: 08/12/2017

---
# <a name="deploying-a-data-processing-extension-to-a-report-server"></a>部署到报表服务器的数据处理扩展插件
  报表服务器使用数据处理扩展插件来检索和处理所呈现报表中的数据。 您应将数据处理扩展插件程序集作为私有程序集部署到报表服务器。 还需要在报表服务器配置文件 RSReportServer.config 中生成一个条目。  
  
## <a name="procedures"></a>过程  
  
#### <a name="to-deploy-a-data-processing-extension-assembly"></a>部署数据处理扩展插件程序集  
  
1.  将程序集从临时位置复制到您要在其上使用数据处理扩展插件的报表服务器的 bin 目录中。 报表服务器 bin 目录的默认位置为 %ProgramFiles%\Microsoft SQL Server\MSRS10_50。\<*实例名称*> services\reportserver\bin。  
  
    > [!NOTE]  
    >  此步骤会妨碍升级到较新的 SQL Server 实例。 有关详细信息，请参阅 [Upgrade and Migrate Reporting Services](../../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)。  
  
2.  在复制程序集文件后，打开 RSReportServer.config 文件。 RSReportServer.config 文件位于 ReportServer 目录中。 还需要在配置文件中为数据处理扩展插件程序集文件生成一个条目。 可以使用 Visual Studio 或诸如记事本之类的简单文本编辑器中打开配置文件。  
  
3.  在 RSReportServer.config 文件中找到 **Data** 元素。 应当在以下位置为新创建的数据处理扩展插件生成一个条目：  
  
    ```  
    <Extensions>  
       <Data>  
          <Your extension configuration information goes here>  
       </Data>  
    </Extensions>  
    ```  
  
4.  为数据处理扩展插件添加一个条目。 条目应包含**扩展**元素替换为值**名称**和**类型**和可能如下所示：  
  
    ```  
    <Extension Name="ExtensionName" Type="CompanyName.ExtensionName.MyConnectionClass, MyExtensionAssembly" />  
    ```  
  
     值**名称**是数据处理扩展插件的唯一名称。 值**类型**是以逗号分隔的列表，其中包括您实现的类的完全限定的命名空间的条目<xref:Microsoft.ReportingServices.Interfaces.IExtension>和<xref:Microsoft.ReportingServices.DataProcessing.IDbConnection>接口，跟 （不包括.dll 文件扩展名） 程序集的名称。 默认情况下，数据处理扩展插件是可见的。 若要从用户界面（如报表管理器）中隐藏扩展插件，请将 **Visible** 属性添加到 **Extension** 元素，并将其设置为 **false**。  
  
5.  为授予你自定义程序集添加的代码组**FullTrust**扩展的权限。 执行此操作通过将代码组添加到位于 %ProgramFiles%\Microsoft SQL Server 在默认情况下的 rssrvpolicy.config 文件\\< MSRS10_50。\<*实例名称*> \Reporting Services\ReportServer。 代码组可能如下所示：  
  
    ```  
    <CodeGroup class="UnionCodeGroup"  
       version="1"  
       PermissionSetName="FullTrust"  
       Name="MyExtensionCodeGroup"  
       Description="Code group for my data processing extension">  
          <IMembershipCondition class="UrlMembershipCondition"  
             version="1"  
             Url="C:\Program Files\Microsoft SQL Server\MSRS10_50.<Instance Name>\Reporting Services\ReportServer\bin\MyExtensionAssembly.dll"  
           />  
    </CodeGroup>  
    ```  
  
 URL 成员身份只是您可以为数据处理扩展插件选择的众多成员条件之一。 有关代码访问安全的详细信息[!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]，请参阅[安全开发 &#40;Reporting Services &#41;](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md).  
  
## <a name="verifying-the-deployment"></a>验证部署  
 您可以使用 Web 服务 <xref:ReportService2010.ReportingService2010.ListExtensions%2A> 方法来验证是否已将数据处理扩展插件成功部署到报表服务器中。 您也可以打开报表管理器，验证扩展插件是否包括在可用数据源列表中。 有关报表管理器和数据源的详细信息，请参阅[创建、修改和删除共享数据源 (SSRS)](../../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)。  
  
## <a name="see-also"></a>另请参阅  
 [部署数据处理扩展插件](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)   
 [Reporting Services 扩展插件](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [实现数据处理扩展插件](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 扩展库](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
