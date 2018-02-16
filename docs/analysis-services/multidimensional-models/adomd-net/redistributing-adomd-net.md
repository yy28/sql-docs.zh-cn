---
title: "重新分发 ADOMD.NET |Microsoft 文档"
ms.custom: 
ms.date: 02/14/2018
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- ADOMD.NET, redistributing
- redistributing ADOMD.NET
ms.assetid: f8db3c99-0243-4b92-b486-0d8786c264f4
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e4337932ea8ffe9a83d6d899e0d407aebe44dbde
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
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
  
  
