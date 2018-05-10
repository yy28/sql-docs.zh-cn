---
title: 重新分发 ADOMD.NET |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: adomd
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1d4d5f06605f68e830aa945d0b502dcb657211f2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="redistributing-adomdnet"></a>重新分发 ADOMD.NET
  编写使用 ADOMD.NET 的应用程序时，必须将 ADOMD.NET 的相应版本随应用程序一起重新发布。 若要重新发布 ADOMD.NET，请将 ADOMD.NET 安装程序包含在应用程序的安装程序中。  
  
 ADOMD.NET 安装程序和 ADOMD.NET 的最新版本可以在 Microsoft 下载中心的 SQL Server 功能包中找到。  
  
 ADOMD.NET 安装程序将安装中的 ADOMD.NET 文件\<*系统驱动器*>: \Program Files\Microsoft.NET\ADOMD.NET\\*版本号*。  
  
 包含 ADOMD.NET 安装程序后，使应用程序的安装程序启动 ADOMD.NET 安装程序并安装 ADOMD.NET。 此外，根据您的环境，可能需要确保相关的程序集被 SQL Server 信任。  
  
 详细信息：  
  
 [适用于 Microsoft SQL Server 功能包](http://go.microsoft.com/fwlink/?LinkId=389949)  
  
 [Microsoft Connect: ADOMD.NET 依赖关系](http://go.microsoft.com/fwlink/?LinkId=389950)  
  
## <a name="see-also"></a>另请参阅  
 [ADOMD.NET 客户端编程](../../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)   
 [ADOMD.NET 服务器编程](../../../analysis-services/multidimensional-models-adomd-net-server/adomd-net-server-programming.md)  
  
  
