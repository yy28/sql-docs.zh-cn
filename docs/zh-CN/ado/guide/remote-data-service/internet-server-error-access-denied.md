---
title: Internet 服务器错误： 拒绝访问 |Microsoft 文档
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
- access denied error in RDS [ADO]
ms.assetid: e5b43cfa-da8d-430d-a2ab-5443dda47a16
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c8d11a1740800a45dabdb4b3f8169f5971fda197
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="internet-server-error-access-denied"></a>Internet 服务器错误： 访问被拒绝
如果收到此错误，则通常意味着 Microsoft Internet 信息服务 (IIS) 返回以下状态：  
  
 HTTP_STATUS_DENIED 401  
  
 请确保 IIS 访问的目录具有适当的权限。 RDS 可以与在任何一个的三种的密码身份验证模式中运行的 IIS Web 服务器进行通信： 匿名的基本或 NT 质询/响应 （在 Windows 2000 中称为集成 Windows 身份验证）。 此外，Web 服务器必须具有与数据源计算机的权限，如果它是 Windows NT/Windows 2000 的计算机。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="see-also"></a>另请参阅  
 [RDS 基础知识](../../../ado/guide/remote-data-service/rds-fundamentals.md)




