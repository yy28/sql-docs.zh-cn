---
title: "启用到 DCOM 上运行的 DLL |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DLL on DCOM in RDS [ADO]
- DCOM in RDS [ADO]
- business objects in RDS [ADO]
ms.assetid: 5f1c2205-191c-4fb4-9bd9-84c878ea46ed
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4cff076bcec382e3c05917d0a7916d04fc28c8e0
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="enabling-a-dll-to-run-on-dcom"></a>启用在 DCOM 上运行的 DLL
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 以下步骤概述了如何启用业务对象.dll，以使用 DCOM 和 Microsoft Internet 信息服务 (HTTP) 通过组件服务。  
  
1.  在组件服务 mmc 管理单元中创建新的空包。  
  
     将使用组件服务 MMC 管理单元来创建包，将 DLL 添加到此包。 这使得.dll 通过 DCOM，可访问，但它会删除通过 IIS 的可访问性。 (如果在注册表中为.dll，检查**Inproc**密钥现在是否为空; 将激活属性，更高版本中所述设置本主题中，将添加中的值**Inproc**键。)  
  
2.  安装到包中的业务对象。  
  
     -或 -  
  
     导入[提高](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)到包中的对象。  
  
3.  将包的激活属性设置**创建者的进程中**（库应用程序）。  
  
     若要使.dll 可通过 DCOM 和 IIS 的同一计算机上访问，必须在组件服务 MMC 管理单元中组件的激活特性设置。 将属性设置为后**创建者的进程中**，你将注意到， **Inproc**已添加服务器注册表项的组件服务指向代理.dll。  
  
 有关组件服务 （或 Microsoft Transaction 服务，如果你使用的 Windows NT） 的详细信息以及如何执行这些步骤，请访问 Microsoft 事务服务器网站。


