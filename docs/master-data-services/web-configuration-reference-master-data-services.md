---
title: Web 配置参考
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- web configuration file [Master Data Services]
ms.assetid: b8cc9a35-97ab-4fe0-ab4b-c07f13d9793a
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: e9d3cd20fc219a7159de0b271dafcc0e9fb2c3ba
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "73728832"
---
# <a name="web-configuration-reference-master-data-services"></a>Web 配置参考 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 使用 Web.config 文件来包含使 Internet Information Services (IIS) 能够承载 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序和 Web 服务的配置设置。 此 Web.config 文件位于 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 安装路径的 WebApplication 文件夹。 有关路径和权限的详细信息，请参阅[文件夹和文件权限 (Master Data Services)](../master-data-services/folder-and-file-permissions-master-data-services.md)。  
  
## <a name="webconfig-elements"></a>Web.Config 元素  
 Web.config 文件除了包含标准 IIS、.NET Framework [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 、ASP.NET 和 Windows Communication Foundation （WCF）配置元素外，还包含一个自定义元素** \<masterDataServices>**。 下表描述了 Web.config 文件中包括的元素。  
  
|配置元素|说明|  
|---------------------------|-----------------|  
|**masterDataServices**|自定义元素。 将 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web 服务连接到 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 数据库。|  
|**connectionStrings**|ASP.NET 元素。 有关详细信息，请参阅 MSDN Library 中的 [connectionStrings 元素（ASP.NET 设置架构）](https://go.microsoft.com/fwlink/?LinkId=178347) 。|  
|**system.web**|ASP.NET 元素。 有关详细信息，请参阅 MSDN Library 中的 [system.web 元素（ASP.NET 设置架构）](https://go.microsoft.com/fwlink/?LinkId=178348) 。|  
|**阶段**|.NET Framework 元素。 有关详细信息，请[ \<](https://go.microsoft.com/fwlink/?LinkId=178349)参阅 MSDN library 中的启动> 元素。|  
|**时会**|.NET Framework 元素。 有关详细信息，请[ \<](https://go.microsoft.com/fwlink/?LinkId=178350)参阅 MSDN library 中的 runtime> 元素。|  
|**system.codedom**|.NET Framework 元素。 有关详细信息，请[ \<](https://go.microsoft.com/fwlink/?LinkId=178351)参阅 MSDN library 中的 system.object> 元素。|  
|**system.web. extensions**|ASP.NET 元素。 有关详细信息，请参阅 MSDN Library 中的 [system.web.extensions 元素（ASP.NET 设置架构）](https://go.microsoft.com/fwlink/?LinkId=178352) 。|  
|**system.webServer**|包含 IIS 元素的节组。 有关详细信息，请参阅 MSDN Library 中的 [system.webServer 节组 \[IIS 7 设置架构\]](https://go.microsoft.com/fwlink/?LinkId=178353)。|  
|**system.serviceModel**|WCF 元素。 有关详细信息，请[ \<](https://go.microsoft.com/fwlink/?LinkId=178354)参阅 MSDN library 中的 system.servicemodel>。|  
|**system.diagnostics**|.NET Framework 元素。 有关详细信息，请[ \<](https://go.microsoft.com/fwlink/?LinkId=178355)参阅 MSDN library 中的 "系统诊断> 元素"。|  
|**appSettings**|ASP.NET 元素。 有关详细信息，请参阅 MSDN Library 中的 [appSettings 元素（常规设置架构）](https://go.microsoft.com/fwlink/?LinkId=178356) 。|  
  
## <a name="masterdataservices-element"></a>masterDataServices 元素  
 MasterDataServices>元素是一个自定义元素，用于将[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web 服务连接到[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]数据库。 ** \<**  
  
### <a name="syntax"></a>语法  
  
```  
<masterDataServices>  
   <instance virtualPath="path" siteName="name" connectionName="name" serviceName="name" />  
</masterDataServices>  
```  
  
### <a name="elements-and-attributes"></a>元素和属性  
  
|项|说明|  
|----------|-----------------|  
|**实例**|子元素。 包含指定 Web 服务和数据库连接字符串信息的属性。|  
|**virtualPath**|属性。 指定 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序和服务的虚拟路径。 这对应于 IIS applicationhost.config 文件中** \<site>** 元素下** \<应用程序>** 元素的**path**属性。|  
|**名**|属性。 指定承载 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序和服务的站点的名称。 这对应于 IIS applicationhost.config 文件中 " ** \<站点>** 下的** \<站点>** 元素的**名称**属性。|  
|**connectionName**|属性。 指定要使用的连接的名称。 这与 web.config 中** \<connectionStrings>** 元素下的** \<add>** 元素的**name**属性相对应。|  
|**serviceName**|属性。 指定 Web 服务的名称。 这对应于 web.config 中** \<服务>** 元素下的** \<服务>** 元素的**name**属性。|  
  
### <a name="example"></a>示例  
 下面的示例演示了 Contoso 站点上一个名为 MDS1 的服务和使用由 MDSDB 指定的连接字符串的 /MDS 路径。  
  
```  
<masterDataServices>  
   <instance virtualPath="/MDS" siteName="Contoso" connectionName="MDSDB" serviceName="MDS1" />  
</masterDataServices>  
```  
  
  
