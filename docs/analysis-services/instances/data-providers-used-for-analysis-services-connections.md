---
title: 用于 Analysis Services 连接的数据提供程序 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f5ba97f90b877896d68cd62598f11d0845fb698e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209531"
---
# <a name="client-libraries-data-providers-used-for-analysis-services-connections"></a>用于 Analysis Services 连接的客户端库 （数据访问接口）
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

Analysis Services 提供了三个客户端库，也称为**数据提供程序**、 为服务器和数据访问工具和客户端应用程序。 SSMS 和 SSDT 和应用程序，例如 Power BI Desktop 和 Excel 连接到 Analysis Services 通过使用这些库等工具。 两个客户端库，ADOMD.NET 和 Analysis Services 管理对象 (AMO)，是托管客户端库。 Analysis Services OLE DB 提供程序 (MSOLAP DLL) 是一个本机客户端库。 客户端库是针对 SQL Server Analysis Services 和 Azure Analysis Services 相同的。
  
##  <a name="bkmk_downloadsite"></a> 从何处获取较新版本  
 客户端计算机上安装的版本应与提供数据的服务器的主要版本匹配。 如果服务器版本比在网络中工作站上安装的数据访问接口版本新，您可能需要安装较新的库。  

客户端库在早期的 SQL Server 功能包包含对应于该 SQL 版本;不过，它们可能不是最新版本。 连接到 Azure Analysis Services 可能需要更高版本。 所有版本都是向后兼容。

若要获取最新版本，请参阅[用于连接到 Azure Analysis Services 客户端库](https://docs.microsoft.com/azure/analysis-services/analysis-services-data-providers)。 
  
## <a name="see-also"></a>请参阅  
 [连接到 Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  
