---
title: "创建 Master Data Manager Web Service Proxy Classes |Microsoft 文档"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 8bdab026-a0c0-41f3-9d36-f3919c23247f
caps.latest.revision: 8
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a45cd15ced90aef95feb03f8fbaafd5aa70cb746
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="create-master-data-manager-web-service-proxy-classes"></a>创建主数据管理器 Web 服务代理类
  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 服务可让您通过任何能访问 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 网站的计算机以编程方式使用 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] 的功能。 在开始编写访问 Web 服务的代码之前，必须先生成代理类。 您用于执行 Web 服务操作的主代理类是 <xref:Microsoft.MasterDataServices.ServiceClient> 类，它可实现 <xref:Microsoft.MasterDataServices.IService> 接口。  
  
## <a name="enable-web-service-metadata-publishing"></a>启用 Web 服务元数据发布  
 在可以生成代理类之前，必须启用 Web 服务元数据发布。 请按照下列步骤完成此操作：  
  
1.  打开[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]在文本编辑器中的 Web.config 文件。 此文件位于 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 安装路径的 WebApplication 文件夹中。  
  
2.  查找**mdsWsHttpBehavior**部分下 **\<serviceBehaviors >**。 有关 **\<serviceMetadata >**元素，设置**httpGetEnabled**到**true**。  
  
    > [!NOTE]  
    >  如果你想要启用通过安全套接字层 (SSL) 的 Web 服务，设置**httpsGetEnabled**到**true**中**mdsWsHttpBehavior** web.config 文件的部分。 你还需要更改**mdsWsHTTPBinding** ，以便为 SSL，同样，并注释掉的非 SSL 部分配置它。  
  
3.  保存对文件的更改。  
  
4.  通过浏览到服务 URL，例如测试元数据发布： `http://yourserver/MDS/service/service.svc`。 如果启用元数据发布，则会显示一个以   
    “您已创建服务”开头的页面。  
  
## <a name="creating-proxy-classes-by-using-visual-studio"></a>通过使用 Visual Studio 创建代理类  
 如果你已安装的 Visual Studio 2010，生成代理类的最简单方法是添加**服务引用**到你的项目。 服务引用的地址为 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web 应用程序的 URL，后面追加 /service/service.svc。 例如： `http://yourserver/MDS/service/service.svc`。 有关详细信息，请参阅[如何： 添加、 更新或移除服务引用](http://go.microsoft.com/fwlink/?LinkId=221167)。  
  
## <a name="creating-proxy-classes-by-using-svcutilexe"></a>使用 Svcutil.exe 创建代理类  
 你必须具有[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]或[!INCLUDE[msCoName](../../includes/msconame-md.md)]以便 Svcutil.exe 具有您的计算机上安装 Windows SDK。 如果使用 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，必须使用 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 命令提示符运行该命令。 有关详细信息，请参阅[ServiceModel 元数据实用工具 (Svcutil.exe)](http://go.microsoft.com/fwlink/?LinkId=165027)和[从服务元数据生成 WCF 客户端](http://go.microsoft.com/fwlink/?LinkId=164821)。  
  
 若要使用 Svcutil.exe 创建一组 C# 代理类，请使用如下命令：  
  
```  
svcutil.exe http://<server_name:port>/<virtual_path>/Service/Service.svc   
/out:<proxy_name>.cs /messageContract /tcv:Version35   
/noconfig /ct:System.Collections.ObjectModel.Collection`1   
/namespace:*,Microsoft.MasterDataServices  
```  
  
 其中：  
  
-   *servername*:*端口*是计算机名和端口号的计算机的承载[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]。  
  
-   *virtual_path*的虚拟路径[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]在 Internet 信息服务 (IIS)。  
  
-   *proxy_name*是生成的代理文件的名称。  
  
## <a name="see-also"></a>另请参阅  
 [已分类的 Web 服务操作 &#40;Master Data Services &#41;](../../master-data-services/develop/categorized-web-service-operations-master-data-services.md)  
  
  
