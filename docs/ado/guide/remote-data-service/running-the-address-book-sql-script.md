---
title: "运行地址簿 SQL 脚本 |Microsoft 文档"
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
ms.assetid: 409b3f8b-0ced-4867-acbe-b245dcdf6702
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4751361a50f4fe594ad4ffc9d4233b41a4918361
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="running-the-address-book-sql-script"></a>运行地址簿 SQL 脚本
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 必须使用 ISQL/查询分析器中的命令行实用工具或 SQL Server 企业管理器到运行包含的 SQL 脚本 (Sampleemp.sql):  
  
-   创建一个新的数据库，AddrBookDB，默认设备上。  
  
-   连接到数据库，AddrBookDB。  
  
-   创建员工表。  
  
-   将填充具有示例数据的表。  
  
-   运行一个简单的 SELECT 语句来验证数据库表的填充。  
  
-   将一个名为"adcdemo"使用密码"adcdemo。"的用户帐户设置  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-65"></a>若要运行 Microsoft SQL Server 6.5 Sampleemp.sql 脚本  
  
1.  单击**启动**，指向**程序**，然后指向**Microsoft SQL Server 6.5**。 单击**SQL 企业管理器**。  
  
2.  从**工具**菜单上，单击**SQL 查询工具**。  
  
3.  单击**负载 SQL 脚本**并浏览到 c:\Platform SDK\Samples\DataAccess\RDS\AddressBook。  
  
4.  选择 Sampleemp.sql 的文件。 单击 **“打开”**。  
  
5.  单击**执行查询**按钮 （在工具栏上的绿色箭头）。  
  
6.  它执行后，关闭**查询**和**企业管理器**windows。  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-70"></a>若要在 Microsoft SQL Server 7.0 中运行 Sampleemp.sql 脚本  
  
1.  单击**启动**，指向**程序**，然后指向**Microsoft SQL Server 7.0**。 单击**企业管理器**。  
  
2.  请确保你想要使用 SQL Server 已选中从已注册的服务器在企业管理器的列表。  
  
3.  从**工具**菜单上，单击**SQL Server 查询分析器**。  
  
4.  单击**负载 SQL 脚本**按钮 （在工具栏上打开的文件夹） 并浏览到 c:\Platform SDK\Samples\DataAccess\RDS\AddressBook。  
  
5.  选择 Sampleemp.sql 的文件。 单击 **“打开”**。  
  
6.  单击**执行查询**按钮 （在工具栏上的绿色箭头） 或**F5**。  
  
7.  它执行后，关闭**查询**，**查询分析器**，和**企业管理器**windows。  
  
## <a name="see-also"></a>另请参阅  
 [运行通讯簿示例应用程序](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)



