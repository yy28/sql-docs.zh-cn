---
title: "服务提供程序和组件 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
- service providers [ADO]
ms.assetid: 1fd7a374-587b-4ca9-9204-3a4019b67a71
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 61232bd2d028c9beb1b5471bb6db0b1c28b7b7e7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="service-providers-and-components"></a>服务提供商和组件
服务提供程序是通过实现由数据存储不以本机方式支持的扩展的接口扩展数据提供程序的功能的组件。  
  
 通用数据访问提供*组件体系结构*各个专门的组件来实现几组离散的数据库功能或"服务，"允许能力较小的存储区上。 因此，而不是强制实施每个数据存储区提供其自己的扩展功能的实现，或强制通用应用程序在内部实现的数据库功能，服务组件提供的常见实现的任何应用程序可以访问任何数据存储区时使用。 某些功能本机实现，可以通过在数据存储和一些通过泛型组件的事实是透明的应用程序。  
  
 例如，游标引擎，如[光标服务用于 OLE DB](http://msdn.microsoft.com/en-us/57638feb-4ecd-4051-becb-8f828d21cf44)，是一个可以使用从要生成可滚动的数据的顺序、 只进的数据存储的数据的服务组件。 而经常使用 ADO 的其他服务提供程序包括[Microsoft OLE DB 永久性提供程序 （ADO 服务提供商）](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) （有关将数据保存到文件），[用于 OLE DB （ADO 服务提供程序） 的 Microsoft 数据调整服务](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (有关分层**记录集**)，和[Microsoft OLE DB 远程处理提供程序 （ADO 服务提供商）](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md) （用于调用远程计算机上的数据提供程序）。  
  
 有关服务和数据提供程序的详细信息，请参阅[附录 a： 提供程序](../../../ado/guide/appendixes/appendix-a-providers.md)。
