---
title: 启用 DCOM 上运行的 DLL |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DLL on DCOM in RDS [ADO]
- DCOM in RDS [ADO]
- business objects in RDS [ADO]
ms.assetid: 5f1c2205-191c-4fb4-9bd9-84c878ea46ed
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9ea7ea83219780602f8d8d68e5c807178e775bc2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922704"
---
# <a name="enabling-a-dll-to-run-on-dcom"></a>允许 DCOM 在 DLL 上运行
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 以下步骤概述如何让业务对象.dll，以使用 DCOM 和 Microsoft Internet 信息服务 (HTTP) 通过组件服务。  
  
1.  在组件服务 MMC 管理单元中创建新的空包。  
  
     将使用组件服务 MMC 管理单元来创建包，然后将 DLL 添加到此包。 这使该.dll 可通过 DCOM 访问，但它会删除通过 IIS 可访问性。 (如果在注册表中为.dll 文件，检查**Inproc**密钥现在是否为空; 将激活属性，更高版本中所述设置本主题中，将添加中的值**Inproc**键。)  
  
2.  安装到包的业务对象。  
  
     -或-  
  
     导入[提高](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)到包的对象。  
  
3.  将包的激活属性设置**创建者的进程中**（库应用程序）。  
  
     若要使.dll 文件可以通过 DCOM 和 IIS 的同一计算机上访问，必须在组件服务 MMC 管理单元中设置组件的激活属性。 将属性设置为后**中创建者的进程**，您会注意**Inproc**已添加到组件服务点代理项.dll 服务器注册表项的。  
  
 组件服务 （或 Microsoft 事务服务，如果您使用的 Windows NT） 有关详细信息，以及如何执行这些步骤，请访问 Microsoft 事务 Server Web 站点。


