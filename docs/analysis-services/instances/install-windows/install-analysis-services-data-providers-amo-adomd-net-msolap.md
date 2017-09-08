---
title: "安装 Analysis Services 数据提供程序 (AMO、 ADOMD.NET、 MSOLAP) |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a7aedabc-6af9-4698-a7a4-98f894001476
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bd6aa812228cce132b4180a8537ba853f3ea92a2
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="install-analysis-services-data-providers-amo-adomdnet-msolap"></a>安装 Analysis Services 数据提供程序（AMO、ADOMD.NET、MSOLAP）
  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 是 Analysis Services 数据提供程序的版本更新，由ADOMD.Net、AMO 和 MSOLAP 组成。  
  
 对于大多数基于查询的数据访问方案中，可以使用已安装在客户端系统上的现有旧版数据提供程序访问 SQL Server 2016 Analysis Services 实例上的表格和多维模型，其中包括使用 SQL Server 2016 专有的功能的表格模型。 作为通用规则，在访问 Analysis Service 模型时，生成查询的客户端应用程序（如 Excel、Reporting Services 或 Tableau）不需要最新的数据提供程序。  
  
 至少就数据提供程序的版本要求而言，建模和管理工具是该规则的例外情况。 这些工具必须具有为目标服务器专门生成的数据提供程序，以便对该服务器上的对象进行操作。 幸运的是，随 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 一起传送的工具自动包括符合当前版本的服务器数据提供程序。  适用于 Visual Studio 2015 的 SQL Server Data Tools 的安装程序可为 SQL Server 2016 Analysis Services 安装数据提供程序。 同样，SQL Server 2016 Management Studio，使用 AMO 和 ADOMD.Net，安装针对 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]的两个数据提供程序。  
  
 确实需要手动安装数据提供程序的一种情况是，自定义使用 Analysis Services 管理对象 (AMO) 的应用程序或脚本。 此版本引入了重构命名空间，该命名空间将主要对象（如服务器和数据库）移到新的命名空间 (Microsoft.AnalysisServices.Core)，后者是 Microsoft.AnalysisServices.dll 程序集的一部分。 如果具有使用 AMO 的自定义代码或脚本，则需要重新编译代码并手动更新每个服务器和客户端工作站（通过 AMO 直接连接到 Analysis Services 的 SQL Server 2016 实例）上的 AMO。  
  
## <a name="provider-list"></a>提供程序列表  
 下表对各提供程序进行了说明。  
  
||||  
|-|-|-|  
|提供程序|Filename|版本|  
|Analysis Services 管理对象 (AMO)|Microsoft.AnalysisServices.dll|13.0.0.0|  
|Analysis Services Core|Microsoft.AnalysisServices.Core.dll|13.0.0.0|  
|Analysis Services (ADOMD.NET)|Microsoft.AnalysisServices.AdomdClient.dll|13.0.0.0|  
|Analysis Services 的 OLE DB 提供程序 (MSOLAP)|MSOLAP130.dll|13.0.0.0|  
  
## <a name="download-and-install-data-provider"></a>下载并安装数据提供程序  
  
1.  转到 [SQL Server 2016 功能包下载页](http://go.microsoft.com/fwlink/?LinkID=398150)。  
  
2.  单击“下载”  以启用各个组件的安装。  
  
3.  对于 64 位计算机，请选择下面全部或部分内容（否则选择 x86 等效对象）：  
  
    -   ENU\x64\SQL_AS_ADOMD.msi  
  
    -   ENU\x64\SQL_AS_AMO.msi  
  
    -   ENU\x64\SQL_AS_OLEDB.msi  
  
4.  单击“下一步”  以下载这些文件。  
  
5.  运行每个程序以安装提供程序。 ADO、MD 和 AMO 程序集安装在 C:\Windows\assembly\GAC_MSIL。 Analysis Services OLE DB 提供程序安装在 C:\Program Files\Microsoft Analysis Services\AS OLEDB\130。  
  
## <a name="verify-installation"></a>验证安装  
  
1.  在文件资源管理器中，转到 C:\Windows\Assembly。  
  
2.  右键单击 Microsoft.AnalysisServices 并选择“属性”。  
  
3.  单击“版本”  以确认你拥有最新版本。  
  
  
