---
title: "用于 Analysis Services 连接的数据提供程序 |Microsoft 文档"
ms.custom: 
ms.date: 12/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 128f6dde-409d-4c12-9820-3305bab57b75
caps.latest.revision: "19"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 7be1179fb84b98aa7610e76015cb957d5f18514a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="client-libraries-data-providers-used-for-analysis-services-connections"></a>用于 Analysis Services 连接的客户端库 （数据访问接口）
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

Analysis Services 提供三个客户端库，也称为**数据提供程序**、 服务器和数据从工具和客户端应用程序的访问。 工具，如 SSMS 和 SSDT 和如同 Power BI Desktop 和 Excel 连接到 Analysis Services 通过使用这些库的应用程序。 两个客户端库，ADOMD.NET 和 Analysis Services 管理对象 (AMO)，是托管客户端库。 Analysis Services OLE DB 提供程序 (MSOLAP DLL) 是一个本机客户端库。 
  
##  <a name="bkmk_downloadsite"></a>从何处获取较新版本  
 在客户端计算机上安装的版本应与提供数据的服务器的主版本相同。 如果服务器版本比在网络中工作站上安装的数据访问接口版本新，您可能需要安装较新的库。  

早期的 SQL Server 功能包中包含的客户端库对应于该 SQL 版本;但是，它们可能不是最新。 连接到 Azure Analysis Services 可能需要更高版本。 所有版本都是向后兼容。

若要获取最新，请参阅[用于连接到 Azure Analysis Services 的客户端库](https://docs.microsoft.com/azure/analysis-services/analysis-services-data-providers)。 
  
## <a name="see-also"></a>另请参阅  
 [连接到 Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  
