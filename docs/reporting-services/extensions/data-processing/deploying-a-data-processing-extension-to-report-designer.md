---
title: "如何： 将数据处理扩展插件部署到报表设计器 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
ms.assetid: 3614e601-004e-4a16-8388-836ffd67e9dd
caps.latest.revision: 41
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: e5e309ee7092bdc64efa89fa27579e9e8944da14
ms.contentlocale: zh-cn
ms.lasthandoff: 08/12/2017

---
# <a name="deploying-a-data-processing-extension-to-report-designer"></a>部署数据处理扩展插件以报表设计器
  报表设计器在您设计报表时使用数据处理扩展插件检索和处理数据。 您应将数据处理扩展插件程序集作为专用程序集部署到报表设计器。 还需要在报表设计器配置文件 RSReportDesigner.config 中生成一个条目。  
  
#### <a name="to-deploy-a-data-processing-extension-assembly"></a>部署数据处理扩展插件程序集  
  
1.  将程序集从临时位置复制到报表设计器目录中。 报表服务器目录的默认位置为 C:\Program Files\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies。  
  
2.  在复制程序集文件后，打开 RSReportDesigner.config 文件。 RSReportDesigner.config 文件也位于报表设计器目录中。 还需要在配置文件中为数据处理扩展插件程序集文件生成一个条目。 你可以打开具有的配置文件[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]或诸如记事本之类的简单文本编辑器。  
  
3.  在 RSReportDesigner.config 文件中找到 **Data** 元素。 应当在以下位置为新创建的数据处理扩展插件生成一个条目：  
  
    ```  
    <Extensions>  
       <Data>  
          <Your extension configuration information goes here>  
       </Data>  
    </Extensions>  
    ```  
  
4.  为你的数据处理扩展插件，其中包括添加一个条目**扩展**元素替换为值**名称**，**类型**，和**可见**属性。 您的条目可能如下所示：  
  
    ```  
    <Extension Name="ExtensionName" Type="CompanyName.ExtensionName.MyConnectionClass, AssemblyName" />  
    ```  
  
     值**名称**是数据处理扩展插件的唯一名称。 值**类型**是以逗号分隔的列表，其中包括您实现的类的完全限定的命名空间的条目<xref:Microsoft.ReportingServices.Interfaces.IExtension>和<xref:Microsoft.ReportingServices.DataProcessing.IDbConnection>接口，跟 （不包括.dll 文件扩展名） 程序集的名称。 默认情况下，数据处理扩展插件是可见的。 若要隐藏用户界面，如报表设计器中，从扩展插件将添加**可见**属性设为**扩展**元素，并将其设置为**false**。  
  
5.  最后，为你授予的自定义程序集添加的代码组**FullTrust**扩展的权限。 要完成该操作，将该代码组添加到 rspreviewpolicy.config 文件中即可，该文件在默认情况下位于 C:\Program Files\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies 中。 代码组可能如下所示：  
  
    ```  
    <CodeGroup class="UnionCodeGroup"  
       version="1"  
       PermissionSetName="FullTrust"  
       Name="MyExtensionCodeGroup"  
       Description="Code group for my data processing extension">  
          <IMembershipCondition class="UrlMembershipCondition"  
             version="1"  
             Url="C:\Program Files\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies\MyExtensionAssembly.dll"  
           />  
    </CodeGroup>  
    ```  
  
 URL 成员身份只是您可以为数据处理扩展插件选择的众多成员条件之一。 有关代码访问安全的详细信息[!INCLUDE[ssRSversion2005](../../../includes/ssrsversion2005-md.md)]，请参阅[安全开发 &#40;Reporting Services &#41;](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md)  
  
## <a name="generic-query-designer"></a>通用查询设计器  
 报表设计器提供了可用于自定义数据处理扩展插件的通用查询设计器。 该设计器包含两个窗格：查询窗格和结果窗格。 您可以使用该通用设计器编写图形界面不支持的查询。 与图形查询设计器不同的是，通用查询设计器不检查查询语法或调整查询的结构。  
  
#### <a name="to-enable-the-generic-query-designer-for-a-custom-extension"></a>为自定义扩展插件启用通用查询设计器  
  
-   将以下条目添加到 RSReportDesigner.config 文件在下**设计器**元素，替换**名称**具有你在以前的条目中提供的名称属性。  
  
    ```  
    <Extension Name="ExtensionName" Type="Microsoft.ReportingServices.QueryDesigners.GenericQueryDesigner,Microsoft.ReportingServices.QueryDesigners"/>  
    ```  
  
## <a name="verifying-the-deployment"></a>验证部署  
 必须先关闭本地计算机上的所有 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 实例，然后才能验证部署。 结束所有当前会话之后，可以在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中创建一个新报表项目，以验证数据处理扩展插件是否已成功部署到报表设计器。 为报表创建新的数据集时，您的扩展插件应当包括在可用数据源类型列表中。  
  
## <a name="see-also"></a>另請參閱  
 [部署数据处理扩展插件](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)   
 [Reporting Services 扩展插件](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [实现数据处理扩展插件](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 扩展库](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

