---
title: 创建主数据管理器 Web 服务代理类
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 8bdab026-a0c0-41f3-9d36-f3919c23247f
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 2e204b5021cb2928988331c73750821225a4192d
ms.sourcegitcommit: 66407a7248118bb3e167fae76bacaa868b134734
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81728433"
---
# <a name="create-master-data-manager-web-service-proxy-classes"></a>创建主数据管理器 Web 服务代理类

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 服务可让您通过任何能访问 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 网站的计算机以编程方式使用 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 的功能。 在开始编写访问 Web 服务的代码之前，必须先生成代理类。 您用于执行 Web 服务操作的主代理类是 <xref:Microsoft.MasterDataServices.ServiceClient> 类，它可实现 <xref:Microsoft.MasterDataServices.IService> 接口。  
  
## <a name="enable-web-service-metadata-publishing"></a>启用 Web 服务元数据发布  
 在可以生成代理类之前，必须启用 Web 服务元数据发布。 请按照下列步骤完成此操作：  
  
1.  在文本编辑器中打开 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web.配置文件。 此文件位于 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 安装路径的 WebApplication 文件夹中。  
  
2.  查找 \<serviceBehaviors> 下的 mdsWsHttpBehavior 部分********。 对于**\<服务元数据>** 元素，将**httpGetEnabled**设置为**true**。  
  
    > [!NOTE]  
    >  如果要通过传输层安全 （TLS）启用 Web 服务（以前称为安全套接字层 （SSL），请将**httpsGetEnabled**设置为**true，** 在 Web.config 文件的**mdsWsHttpBehavior**部分。 您还需要更改**mdsWsHTTPBinding，** 以便它也可以配置为 TLS，并注释掉非 TLS 部分。  
  
3.  保存对文件的更改。  
  
4.  通过浏览服务 URL 来测试元数据发布，例如：`https://yourserver/MDS/service/service.svc`。 如果启用元数据发布，则会显示一个以   
    “你已创建服务”开头的页面。  
  
## <a name="creating-proxy-classes-by-using-visual-studio"></a>通过使用 Visual Studio 创建代理类  
 如果已安装了 Visual Studio 2010，则生成代理类的最简方法是将“服务引用”添加到项目中****。 服务引用的地址为 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 应用程序的 URL，后面追加 /service/service.svc。 例如：`https://yourserver/MDS/service/service.svc`。 有关详细信息，请参阅[如何添加、更新或删除服务引用](https://go.microsoft.com/fwlink/?LinkId=221167)。  
  
## <a name="creating-proxy-classes-by-using-svcutilexe"></a>使用 Svcutil.exe 创建代理类  
 您必须安装或[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]安装[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows SDK 才能在计算机上安装 Svcutil.exe。 如果使用 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，必须使用 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 命令提示符运行该命令。 有关详细信息，请参阅 [ServiceModel 元数据实用工具 (Svcutil.exe)](https://go.microsoft.com/fwlink/?LinkId=165027) 和[根据服务元数据生成 WCF 客户端](https://go.microsoft.com/fwlink/?LinkId=164821)。  
  
 若要使用 Svcutil.exe 创建一组 C# 代理类，请使用如下命令：  
  
```  
svcutil.exe https://<server_name:port>/<virtual_path>/Service/Service.svc   
/out:<proxy_name>.cs /messageContract /tcv:Version35   
/noconfig /ct:System.Collections.ObjectModel.Collection`1   
/namespace:*,Microsoft.MasterDataServices  
```  
  
 其中：  
  
-   servername:port 是承载 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 的计算机名称和端口号****。  
  
-   virtual_path 是 Internet 信息服务 (IIS) 中 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 的虚拟路径**。  
  
-   proxy_name 是生成的代理文件名称**。  
  
## <a name="see-also"></a>另请参阅  
 [分类的 Web 服务操作 &#40;Master Data Services&#41;](../../master-data-services/develop/categorized-web-service-operations-master-data-services.md)  
  
  
