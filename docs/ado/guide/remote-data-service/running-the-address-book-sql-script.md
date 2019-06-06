---
title: 运行通讯簿 SQL 脚本 |Microsoft Docs
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
ms.assetid: 409b3f8b-0ced-4867-acbe-b245dcdf6702
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 366e1a5812b4d8152e5c8965d3059e3a6b2ca1cb
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704194"
---
# <a name="running-the-address-book-sql-script"></a>运行通讯簿 SQL 脚本
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 必须使用 ISQL/查询分析工具命令行实用工具或 SQL Server 企业管理器到运行包含的 SQL 脚本 (Sampleemp.sql):  
  
-   默认设备上创建一个新的数据库，AddrBookDB。  
  
-   连接到数据库，AddrBookDB。  
  
-   创建员工表。  
  
-   示例使用数据填充表。  
  
-   运行一个简单的 SELECT 语句来验证对数据库表的填充。  
  
-   设置了名为"adcdemo"，密码为"adcdemo。"的用户帐户  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-65"></a>若要在 Microsoft SQL Server 6.5 中运行 Sampleemp.sql 脚本  
  
1.  单击**启动**，依次指向**程序**，然后指向**Microsoft SQL Server 6.5**。 单击**SQL 企业管理器**。  
  
2.  从**工具**菜单上，单击**SQL 查询工具**。  
  
3.  单击**负载 SQL 脚本**并浏览到 c:\Platform SDK\Samples\DataAccess\RDS\AddressBook。  
  
4.  选择文件 Sampleemp.sql。 单击 **“打开”** 。  
  
5.  单击**执行查询**按钮 （工具栏上的绿色箭头）。  
  
6.  它执行后，关闭**查询**并**企业管理器**windows。  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-70"></a>若要在 Microsoft SQL Server 7.0 中运行 Sampleemp.sql 脚本  
  
1.  单击**启动**，依次指向**程序**，然后指向**Microsoft SQL Server 7.0**。 单击**企业管理器**。  
  
2.  为确保已注册的服务器在企业管理器的列表中选择你想要使用 SQL Server。  
  
3.  从**工具**菜单上，单击**SQL Server 查询分析器**。  
  
4.  单击**负载 SQL 脚本**按钮 （在工具栏上打开的文件夹） 并浏览到 c:\Platform SDK\Samples\DataAccess\RDS\AddressBook。  
  
5.  选择文件 Sampleemp.sql。 单击 **“打开”** 。  
  
6.  单击**执行查询**按钮 （工具栏上的绿色箭头） 或**F5**。  
  
7.  它执行后，关闭**查询**，**查询分析器**，并**企业管理器**windows。  
  
## <a name="see-also"></a>请参阅  
 [运行通讯簿示例应用程序](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)


