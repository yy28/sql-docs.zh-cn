---
title: "Web 配置参考 (Master Data Services) |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- web configuration file [Master Data Services]
ms.assetid: b8cc9a35-97ab-4fe0-ab4b-c07f13d9793a
caps.latest.revision: 6
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1be0e90d7d2ba9b2751677015957ca249d91119e
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="web-configuration-reference-master-data-services"></a>Web 配置参考 (Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]使用 Web.config 文件以包含到主机中启用 Internet 信息服务 (IIS) 的配置设置[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]Web 应用程序和 Web 服务。 此 Web.config 文件位于 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 安装路径的 WebApplication 文件夹。 有关路径和权限的详细信息，请参阅[文件夹和文件权限 (Master Data Services)](../master-data-services/folder-and-file-permissions-master-data-services.md)。  
  
## <a name="webconfig-elements"></a>Web.Config 元素  
 Web.config 文件包含一个自定义[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]元素，  **\<masterDataServices >**，除了标准的 IIS、.NET Framework、 ASP.NET 和 Windows Communication Foundation (WCF) 配置元素。 下表描述了 Web.config 文件中包括的元素。  
  
|配置元素|Description|  
|---------------------------|-----------------|  
|**masterDataServices**|自定义元素。 将 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web 服务连接到 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库。|  
|**connectionStrings**|ASP.NET 元素。 有关详细信息，请参阅 MSDN Library 中的 [connectionStrings 元素（ASP.NET 设置架构）](http://go.microsoft.com/fwlink/?LinkId=178347) 。|  
|**system.web**|ASP.NET 元素。 有关详细信息，请参阅 MSDN Library 中的 [system.web 元素（ASP.NET 设置架构）](http://go.microsoft.com/fwlink/?LinkId=178348) 。|  
|**startup**|.NET Framework 元素。 有关详细信息，请参阅[\<启动 > 元素](http://go.microsoft.com/fwlink/?LinkId=178349)MSDN 库中。|  
|**运行库**|.NET Framework 元素。 有关详细信息，请参阅[\<运行时 > 元素](http://go.microsoft.com/fwlink/?LinkId=178350)MSDN 库中。|  
|**system.codedom**|.NET Framework 元素。 有关详细信息，请参阅[ \<system.codedom > 元素](http://go.microsoft.com/fwlink/?LinkId=178351)MSDN 库中。|  
|**system.web.extensions**|ASP.NET 元素。 有关详细信息，请参阅 MSDN Library 中的 [system.web.extensions 元素（ASP.NET 设置架构）](http://go.microsoft.com/fwlink/?LinkId=178352) 。|  
|**system.webServer**|包含 IIS 元素的节组。 有关详细信息，请参阅 MSDN Library 中的 [system.webServer 节组 \[IIS 7 设置架构\]](http://go.microsoft.com/fwlink/?LinkId=178353)。|  
|**system.serviceModel**|WCF 元素。 有关详细信息，请参阅[ \<system.serviceModel >](http://go.microsoft.com/fwlink/?LinkId=178354) MSDN 库中。|  
|**system.diagnostics**|.NET Framework 元素。 有关详细信息，请参阅[ \<system.diagnostics > 元素](http://go.microsoft.com/fwlink/?LinkId=178355)MSDN 库中。|  
|**appSettings**|ASP.NET 元素。 有关详细信息，请参阅 MSDN Library 中的 [appSettings 元素（常规设置架构）](http://go.microsoft.com/fwlink/?LinkId=178356) 。|  
  
## <a name="masterdataservices-element"></a>masterDataServices 元素  
  **\<MasterDataServices >**元素是可用于连接的自定义元素[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]Web 服务到[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]数据库。  
  
### <a name="syntax"></a>语法  
  
```  
<masterDataServices>  
   <instance virtualPath="path" siteName="name" connectionName="name" serviceName="name" />  
</masterDataServices>  
```  
  
### <a name="elements-and-attributes"></a>元素和属性  
  
|项|Description|  
|----------|-----------------|  
|**instance**|子元素。 包含指定 Web 服务和数据库连接字符串信息的属性。|  
|**virtualPath**|属性。 指定 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序和服务的虚拟路径。 这对应于**路径**属性**\<应用程序 >**元素下的**\<站点 >** IIS ApplicationHost.config 文件中的元素。|  
|**siteName**|属性。 指定承载 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序和服务的站点的名称。 这对应于**名称**属性**\<站点 >**元素下的**\<站点 >** IIS ApplicationHost.config 文件中。|  
|**connectionName**|属性。 指定要使用的连接的名称。 这对应于**名称**属性**\<添加 >**元素下的 **\<connectionStrings >**在 Web.config 中的元素。|  
|**serviceName**|属性。 指定 Web 服务的名称。 这对应于**名称**属性**\<服务 >**元素下的**\<服务 >**在 Web.config 中的元素。|  
  
### <a name="example"></a>示例  
 下面的示例演示了 Contoso 站点上一个名为 MDS1 的服务和使用由 MDSDB 指定的连接字符串的 /MDS 路径。  
  
```  
<masterDataServices>  
   <instance virtualPath="/MDS" siteName="Contoso" connectionName="MDSDB" serviceName="MDS1" />  
</masterDataServices>  
```  
  
  
