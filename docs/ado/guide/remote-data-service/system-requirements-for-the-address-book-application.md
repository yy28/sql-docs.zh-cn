---
title: "系统要求的地址预订应用程序 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: da385405-1c9a-478b-9bf6-fba70015324c
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 070c809c23fcd70c5048e70f61ac74ad4bc7ce4b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="system-requirements-for-the-address-book-application"></a>通讯簿应用程序的系统要求
若要设置通讯簿示例应用程序，需要满足以下软件和数据库要求：  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="software-requirements"></a>软件要求  
 运行此 Web 应用程序的服务器计算机软件要求包括：  
  
-   Microsoft Windows NT® Server 4.0，带有 Service Pack 3 或更高版本或 Microsoft Windows® 2000年服务器。  
  
-   Microsoft Internet 信息服务 (IIS) 版本 3.0 或更高版本，与 Active Server Pages。  
  
 运行此 Web 应用程序的客户端计算机软件要求包括：  
  
-   Microsoft Internet Explorer 4.0 或更高版本。  
  
-   Microsoft Windows NT 4.0 工作站或服务器、 Windows 2000 或 Microsoft Windows 98。  
  
## <a name="database-requirements"></a>数据库要求  
 若要使用此示例，你必须：  
  
-   操作的 Microsoft® SQL Server 6.5 版或更高版本数据库服务器。  
  
-   若要创建数据库并使用示例数据填充它的权限。  
  
-   数据验证的填充通过企业管理器或 ISQL 实用程序 （在 SQL Server 7.0 中调用查询分析器）。  
  
 如果你没有权限，数据库管理员可能需要设置系统并授予你访问的数据库权限，或为你设置数据库。  
  
## <a name="see-also"></a>另请参阅  
 [运行地址簿 SQL 脚本](../../../ado/guide/remote-data-service/running-the-address-book-sql-script.md)   
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [运行通讯簿示例应用程序](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)



