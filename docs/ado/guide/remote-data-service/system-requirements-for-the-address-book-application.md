---
title: 通讯簿应用程序的系统要求 |Microsoft Docs
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
ms.openlocfilehash: 2450cc97229a6629d4c2895f3960e3033d129789
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67922037"
---
# <a name="system-requirements-for-the-address-book-application"></a>通讯簿应用程序的系统要求
若要设置通讯簿示例应用程序，需要满足以下软件和数据库要求：  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件（有关详细信息，请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)）。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="software-requirements"></a>软件要求  
 运行此 Web 应用程序的服务器计算机软件要求包括：  
  
-   Microsoft Windows NT® Server 4.0 Service Pack 3 或更高版本，或者 Microsoft Windows®2000服务器。  
  
-   Microsoft Internet Information Services （IIS）版本3.0 或更高版本，以及 Active Server Pages。  
  
 运行此 Web 应用程序的客户端计算机软件要求包括：  
  
-   Microsoft Internet Explorer 4.0 或更高版本。  
  
-   Microsoft Windows NT 4.0 工作站或服务器、Windows 2000 或 Microsoft Windows 98。  
  
## <a name="database-requirements"></a>数据库要求  
 若要使用此示例，必须具有：  
  
-   Microsoft® SQL Server 版本6.5 或更高版本的数据库服务器。  
  
-   用于创建数据库并在其中填充示例数据的权限。  
  
-   通过企业管理器或 ISQL 实用程序（在 SQL Server 7.0 中称为查询分析器）来验证填充的数据。  
  
 如果你没有权限，则数据库管理员可能需要设置系统，并向你授予对数据库的访问权限，或者为你设置数据库。  
  
## <a name="see-also"></a>另请参阅  
 [运行通讯簿 SQL 脚本](../../../ado/guide/remote-data-service/running-the-address-book-sql-script.md)   
 [DataControl 对象（RDS）](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [运行通讯簿示例应用程序](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)


