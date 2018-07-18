---
title: 重新发布 ADOMD.NET |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ADOMD.NET, redistributing
- redistributing ADOMD.NET
ms.assetid: f8db3c99-0243-4b92-b486-0d8786c264f4
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6fde698740a417076f7fe139250765b9610e91b5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37245607"
---
# <a name="redistributing-adomdnet"></a>重新发布 ADOMD.NET
  编写使用 ADOMD.NET 的应用程序时，必须将 ADOMD.NET 的相应版本随应用程序一起重新发布。 若要重新发布 ADOMD.NET，请将 ADOMD.NET 安装程序包含在应用程序的安装程序中。  
  
 ADOMD.NET 安装程序和 ADOMD.NET 的最新版本可以在 Microsoft 下载中心的 SQL Server 功能包中找到。  
  
 ADOMD.NET 安装程序将安装在将 ADOMD.NET 文件\<*系统驱动器*>: \Program Files\Microsoft.NET\ADOMD.NET\\*版本号*。  
  
 包含 ADOMD.NET 安装程序后，使应用程序的安装程序启动 ADOMD.NET 安装程序并安装 ADOMD.NET。 此外，根据您的环境，可能需要确保相关的程序集被 SQL Server 信任。  
  
 详细信息：    
  
 [Microsoft SQL Server 功能包](http://go.microsoft.com/fwlink/?LinkId=389949)  
  
 [Microsoft Connect: ADOMD.NET 依赖项](http://go.microsoft.com/fwlink/?LinkId=389950)  
  
## <a name="see-also"></a>请参阅  
 [ADOMD.NET 客户端编程](../../multidimensional-models-adomd-net-client/adomd-net-client-programming.md)   
 [ADOMD.NET 服务器编程](../../multidimensional-models-adomd-net-server/adomd-net-server-programming.md)  
  
  
