---
title: "重新分发 ADOMD.NET |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- ADOMD.NET, redistributing
- redistributing ADOMD.NET
ms.assetid: f8db3c99-0243-4b92-b486-0d8786c264f4
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8c87db9dd22e53f8335dcbbb4994cd0835dfafcb
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="redistributing-adomdnet"></a>重新分发 ADOMD.NET
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]当你编写的应用程序将使用 ADOMD.NET 时，必须重新 ADOMD.NET 的适当版本分发随应用程序。 若要重新发布 ADOMD.NET，请将 ADOMD.NET 安装程序包含在应用程序的安装程序中。  
  
 ADOMD.NET 安装程序和 ADOMD.NET 的最新版本可以在 Microsoft 下载中心的 SQL Server 功能包中找到。  
  
 ADOMD.NET 安装程序将安装中的 ADOMD.NET 文件\<*系统驱动器*>: \Program Files\Microsoft.NET\ADOMD.NET\\*版本号*。  
  
 包含 ADOMD.NET 安装程序后，使应用程序的安装程序启动 ADOMD.NET 安装程序并安装 ADOMD.NET。 此外，根据您的环境，可能需要确保相关的程序集被 SQL Server 信任。  
  
 详细信息：  
  
 [适用于 Microsoft SQL Server 功能包](http://go.microsoft.com/fwlink/?LinkId=389949)  
  
 [Microsoft Connect: ADOMD.NET 依赖关系](http://go.microsoft.com/fwlink/?LinkId=389950)  
  
## <a name="see-also"></a>另请参阅  
 [ADOMD.NET 客户端编程](../../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)   
 [ADOMD.NET 服务器编程](../../../analysis-services/multidimensional-models-adomd-net-server/adomd-net-server-programming.md)  
  
  
