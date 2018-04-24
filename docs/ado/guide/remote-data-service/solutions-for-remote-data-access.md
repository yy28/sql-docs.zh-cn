---
title: 远程数据访问的解决方案 |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS [ADO]
ms.assetid: d311cc67-7db7-4c43-9590-d465564695e4
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 84030d05131d8a410690a6896b5173da356240c3
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="solutions-for-remote-data-access"></a>远程数据访问的解决方案
## <a name="the-issue"></a>此问题  
 ADO 使你的应用程序能够直接访问和修改数据源 （有时称为双层系统）。 例如，如果你连接到包含你的数据的数据源，即直接连接两个层系统中。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 但是，你可能想要通过中介如 Microsoft® Internet 信息服务 (IIS) 间接访问数据源。 这种安排有时称为三层系统。 IIS 是提供一种高效方式本地或客户端应用程序可通过调用远程或服务器，程序跨 Internet 或 intranet 的客户端/服务器系统。 服务器程序获得对数据源的访问，并根据需要处理获得的数据。  
  
 例如，你的 intranet Web 页面包含 Microsoft® Visual Basic Scripting Edition (VBScript)，后者将连接到 IIS 中编写的应用程序。 IIS 反过来连接到实际数据源、 检索数据，以某种方式对其进行处理，然后返回到你的应用程序的所处理的信息。  
  
 在此示例中，你的应用程序永远不会直接连接到数据源;IIS 未。 和 IIS 访问通过 ADO 的数据。  
  
> [!NOTE]
>  客户端/服务器应用程序不需要基于 Internet 或 intranet 上 (即，基于 Web 的) — 它可能仅包含在本地网络上编译的程序。 但是，典型情况是基于 Web 的应用程序。  
  
 由于某些可视控件，如网格、 复选框或列表中，可以使用返回的信息，必须由 visual 控件轻松地使用返回的信息。  
  
 所需的简单和高效的应用程序编程接口，它支持三层系统，并返回信息作为轻松就像它已被检索到的双层系统上。 远程数据服务 (RDS) 是这样的接口。  
  
## <a name="the-solution"></a>解决方案  
 RDS 定义了一个编程模型 — 的访问和更新数据源所需的活动序列-若要获取对通过媒介，如 Internet 信息服务 (IIS) 的数据访问。 编程模型总结了 rds.的全部功能。  
  
## <a name="see-also"></a>另请参阅  
 [基本的 RDS 编程模型](../../../ado/guide/remote-data-service/basic-rds-programming-model.md)   
 [RDS 方案](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 教程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [RDS 使用情况和安全性](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


