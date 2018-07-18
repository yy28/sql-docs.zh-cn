---
title: 服务提供商和组件 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
- service providers [ADO]
ms.assetid: 1fd7a374-587b-4ca9-9204-3a4019b67a71
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 085e0caa494baf624468ccb4f4c4bd99020c588b
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2018
ms.locfileid: "38984309"
---
# <a name="service-providers-and-components"></a>服务提供商和组件
服务提供程序是通过实现由数据存储本身不支持的扩展的接口扩展的数据提供程序功能的组件。  
  
 通用数据访问提供*组件体系结构*各个专门的组件来实现几组离散的数据库的功能或"服务，"允许功能较少的存储区上。 因此，而不是强制实施每个数据存储区提供其自己的扩展功能的实现或强制通用应用程序在内部实现的数据库功能，服务组件提供通用的实现的任何应用程序可以访问任何数据存储时使用。 某些功能由数据存储区和通过普通组件以本机方式实现这一事实是透明的应用程序。  
  
 例如，游标引擎，如[用于 OLE DB 的游标服务](http://msdn.microsoft.com/57638feb-4ecd-4051-becb-8f828d21cf44)，是一个服务组件，可使用从连续的只进数据存储来生成可滚动的数据的数据。 通常使用 ADO 的其他服务提供程序包括[Microsoft OLE DB 永久性提供程序 （ADO 服务提供程序）](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) （适用于将数据保存到文件），[用于 OLE DB （ADO 服务提供商） 的 Microsoft Data Shaping 服务](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (对于分层**记录集**)，和[Microsoft OLE DB 远程处理提供程序 （ADO 服务提供商）](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md) （用于调用远程计算机上的数据提供程序）。  
  
 有关服务和数据提供程序的详细信息，请参阅[附录 a： 提供程序](../../../ado/guide/appendixes/appendix-a-providers.md)。
