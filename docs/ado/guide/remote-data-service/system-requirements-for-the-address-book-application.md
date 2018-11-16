---
title: 系统要求的地址预订应用程序 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: da385405-1c9a-478b-9bf6-fba70015324c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10a7097292562acd60e8b83af9a48bd61aeb8557
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/12/2018
ms.locfileid: "51558054"
---
# <a name="system-requirements-for-the-address-book-application"></a>通讯簿应用程序的系统要求
若要设置的通讯簿示例应用程序，需要满足以下软件和数据库要求：  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="software-requirements"></a>软件要求  
 运行此 Web 应用程序的服务器计算机软件要求包括：  
  
-   Microsoft Windows NT® Server 4.0，带有 Service Pack 3 或更高版本或 Microsoft Windows® 2000 Server。  
  
-   Microsoft Internet 信息服务 (IIS) 版本 3.0 或更高版本，与 Active Server Pages。  
  
 运行此 Web 应用程序的客户端计算机软件要求包括：  
  
-   Microsoft Internet Explorer 4.0 或更高版本。  
  
-   Microsoft Windows NT 4.0 工作站或服务器、 Windows 2000 或 Microsoft Windows 98。  
  
## <a name="database-requirements"></a>数据库要求  
 若要使用此示例，必须具有：  
  
-   正常运行的 Microsoft® SQL Server 版本 6.5 或更高版本的数据库服务器。  
  
-   若要创建数据库并使用示例数据填充它的权限。  
  
-   通过企业管理器或 ISQL 实用程序 （称为查询分析器中 SQL Server 7.0） 填充的数据的验证。  
  
 如果您没有权限，数据库管理员可能需要将系统和授予访问权限，到数据库，或将数据库设置为你设置。  
  
## <a name="see-also"></a>请参阅  
 [运行通讯簿 SQL 脚本](../../../ado/guide/remote-data-service/running-the-address-book-sql-script.md)   
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [运行通讯簿示例应用程序](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)


