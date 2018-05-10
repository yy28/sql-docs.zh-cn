---
title: 用于 Analysis Services 连接的数据提供程序 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7703bda267a7b646bf6ccbbfee98c7401599f3a0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="client-libraries-data-providers-used-for-analysis-services-connections"></a>用于 Analysis Services 连接的客户端库 （数据访问接口）
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

Analysis Services 提供三个客户端库，也称为**数据提供程序**、 服务器和数据从工具和客户端应用程序的访问。 工具，如 SSMS 和 SSDT 和如同 Power BI Desktop 和 Excel 连接到 Analysis Services 通过使用这些库的应用程序。 两个客户端库，ADOMD.NET 和 Analysis Services 管理对象 (AMO)，是托管客户端库。 Analysis Services OLE DB 提供程序 (MSOLAP DLL) 是一个本机客户端库。 客户端库是相同的 SQL Server Analysis Services 和 Azure Analysis Services。
  
##  <a name="bkmk_downloadsite"></a> 从何处获取较新版本  
 在客户端计算机上安装的版本应与提供数据的服务器的主版本匹配。 如果服务器版本比在网络中工作站上安装的数据访问接口版本新，您可能需要安装较新的库。  

早期的 SQL Server 功能包中包含的客户端库对应于该 SQL 版本;但是，它们可能不是最新。 连接到 Azure Analysis Services 可能需要更高版本。 所有版本都是向后兼容。

若要获取最新，请参阅[用于连接到 Azure Analysis Services 的客户端库](https://docs.microsoft.com/azure/analysis-services/analysis-services-data-providers)。 
  
## <a name="see-also"></a>另请参阅  
 [连接到 Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  
