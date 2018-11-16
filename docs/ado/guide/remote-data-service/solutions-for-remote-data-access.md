---
title: 远程数据访问解决方案 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS [ADO]
ms.assetid: d311cc67-7db7-4c43-9590-d465564695e4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 302a43238c755890e9fd106d8784eabdd0361d88
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/12/2018
ms.locfileid: "51558614"
---
# <a name="solutions-for-remote-data-access"></a>远程数据访问的解决方案
## <a name="the-issue"></a>此问题  
 ADO 使应用程序可以直接访问和修改数据源 （有时称为两层系统）。 例如，如果你连接到包含你的数据的数据源的两层系统中是直接连接。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 但是，你可能想要通过中介如 Microsoft® Internet 信息服务 (IIS) 间接访问数据源。 这种排列方式有时称为三层系统。 IIS 是一个有效地本地、 或客户端应用程序调用远程或服务器上，程序在 Internet 或 intranet 的客户端/服务器系统。 服务器程序获得数据源访问权，并根据需要处理获得的数据。  
  
 例如，intranet 网页包含在 Microsoft® Visual Basic Scripting Edition (VBScript)，后者将连接到 IIS 中编写的应用程序。 IIS 又连接到实际数据源、 检索数据、 对其进行处理以某种方式，然后将已处理的信息返回到你的应用程序。  
  
 在此示例中，你的应用程序永远不会直接连接到数据源;IIS 未。 和 IIS 通过 ADO 来访问这些数据。  
  
> [!NOTE]
>  客户端/服务器应用程序不需要 Internet 或 intranet 上基于 (即，基于 Web 的)，它可能仅包含本地网络上的已编译程序。 但是，典型的情况是基于 Web 的应用程序。  
  
 某些可视控件，如网格、 复选框或列表中，可能会使用返回的信息，因此必须按可视控件易于使用返回的信息。  
  
 您希望的简单和高效的应用程序编程界面支持三层系统，并返回信息作为轻松像它已被检索到的两层系统上。 远程数据服务 (RDS) 是此接口。  
  
## <a name="the-solution"></a>解决方案  
 RDS 定义了一个编程模型 — 的访问和更新数据源所需的活动序列，以获取通过中介，例如 Internet 信息服务 (IIS) 对数据的访问权限。 编程模型中囊括了整个 rds.的功能  
  
## <a name="see-also"></a>请参阅  
 [基本 RDS 编程模型](../../../ado/guide/remote-data-service/basic-rds-programming-model.md)   
 [RDS 方案](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 教程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [RDS 使用情况和安全性](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


