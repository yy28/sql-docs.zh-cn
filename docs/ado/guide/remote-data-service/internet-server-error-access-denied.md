---
title: Internet 服务器错误： 访问被拒绝 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- access denied error in RDS [ADO]
ms.assetid: e5b43cfa-da8d-430d-a2ab-5443dda47a16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d7932d5d30964e654f86138a02977a27521569b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47681516"
---
# <a name="internet-server-error-access-denied"></a>Internet 服务器错误：拒绝访问
如果收到此错误，这通常意味着 Microsoft Internet 信息服务 (IIS) 返回以下状态：  
  
 HTTP_STATUS_DENIED 401  
  
 请确保通过 IIS 访问的目录拥有适当的权限。 RDS 可以与运行中的三种的密码身份验证模式的任何一个的 IIS Web 服务器进行通信： Anonymous、 Basic 或 NT 质询/响应 （在 Windows 2000 中称为集成 Windows 身份验证）。 此外，Web 服务器必须具有对数据源计算机的权限，如果它是 Windows NT/Windows 2000 的计算机。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/en-us/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="see-also"></a>请参阅  
 [RDS 基础知识](../../../ado/guide/remote-data-service/rds-fundamentals.md)




