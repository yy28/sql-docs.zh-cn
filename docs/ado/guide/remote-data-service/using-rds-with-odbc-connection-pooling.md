---
title: 使用 RDS 与 ODBC 连接池 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connection pooling in RDS [ADO]
ms.assetid: e8b912c1-da5b-4e85-a000-1e6648a94237
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 14f06b98896a63f8e19ce22fb9cd1eb5b181f481
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66699259"
---
# <a name="using-rds-with-odbc-connection-pooling"></a>使用 RDS 与 ODBC 连接池
如果使用 ODBC 数据源，可以使用连接池选项在 Internet 信息服务 (IIS) 以实现高性能的客户端负载的处理。 连接池是资源管理器的连接，维护经常使用的连接的打开状态。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 若要启用连接池，请参阅 Internet Information Services 文档。  
  
 请注意，启用连接池可能会受 Web 服务器的其他限制，如 Microsoft Internet Information Services 文档中所述。  
  
 若要确保连接池是稳定并提供额外的性能提升，必须配置为使用 TCP/IP 套接字网络库的 Microsoft SQL Server。  
  
 若要执行此操作，需要：  
  
-   SQL Server 计算机配置为使用 TCP/IP 套接字。  
  
-   配置要使用 TCP/IP 套接字的 Web 服务器。  
  
## <a name="configuring-the-sql-server-computer-to-use-tcpip-sockets"></a>SQL Server 计算机配置为使用 TCP/IP 套接字  
 SQL Server 计算机上运行 SQL Server 安装程序，以便与数据源之间的交互使用 TCP/IP 套接字网络库。  
  
### <a name="to-specify-the-tcpip-socket-network-library-on-the-sql-server-computer"></a>若要指定 SQL Server 计算机上的 TCP/IP 套接字网络库  
  
### <a name="in-microsoft-sql-server-65"></a>在 Microsoft SQL Server 6.5 中：  
  
1.  从开始菜单中，依次指向程序、 指向 Microsoft SQL Server 6.5、，然后单击 SQL 安装程序。  
  
2.  两次单击继续。  
  
3.  Microsoft SQL Server 中的选项对话框，选择更改网络支持，然后单击继续。  
  
4.  请确保选择 TCP/IP 套接字复选框，然后单击确定。  
  
5.  单击继续以完成，并退出安装程序。  
  
### <a name="in-microsoft-sql-server-70"></a>在 Microsoft SQL Server 7.0:  
  
1.  从开始菜单中，依次指向程序，指向 Microsoft SQL Server 7.0、，然后单击服务器网络实用工具。  
  
2.  在对话框中的常规选项卡上，单击添加。  
  
3.  在添加网络库配置对话框中，单击 TCP/IP。  
  
4.  在端口号和代理地址框中，输入由网络管理员提供的端口号和代理服务器地址。  
  
5.  单击确定以完成，并退出安装程序。  
  
## <a name="configuring-the-web-server-to-use-tcpip-sockets"></a>将 Web 服务器配置为使用 TCP/IP 套接字  
 有两个选项用于配置 Web 服务器，以使用 TCP/IP 套接字。 执行哪些操作取决于是否所有 SQL Server 都访问从 Web 服务器，或仅特定 SQL Server 都访问从 Web 服务器。  
  
 如果所有 SQL Server 从 Web 服务器都访问，需要在 Web 服务器计算机上运行 SQL Server 客户端配置实用工具。 使用以下步骤更改为使用 TCP/IP 套接字网络库通过此 IIS Web 服务器所做的所有 SQL Server 连接的默认网络库。  
  
### <a name="to-configure-the-web-server-all-sql-servers"></a>若要配置 Web 服务器 (所有 SQL Server)  
  
### <a name="for-microsoft-sql-server-65"></a>对于 Microsoft SQL Server 6.5:  
  
1.  从开始菜单中，依次指向程序，指向 Microsoft SQL Server 6.5、，然后单击 SQL 客户端配置实用工具。  
  
2.  单击网络库选项卡。  
  
3.  在默认网络框中，选择 TCP/IP 套接字。  
  
4.  单击完成以保存更改并退出实用程序。  
  
### <a name="for-microsoft-sql-server-70"></a>对于 Microsoft SQL Server 7.0:  
  
1.  从开始菜单中，依次指向程序，指向 Microsoft SQL Server 7.0、，然后单击客户端网络实用工具。  
  
2.  单击常规选项卡。  
  
3.  在默认网络库中，单击 TCP/IP。  
  
4.  单击确定以保存更改并退出实用程序。  
  
 如果从 Web 服务器访问特定的 SQL Server，则需要在 Web 服务器计算机上运行 SQL Server 客户端配置实用工具。 若要更改特定的 SQL Server 连接的网络库，配置 SQL Server 客户端上的软件的 Web 服务器计算机，如下所示。  
  
### <a name="to-configure-the-web-server-a-specific-sql-server"></a>若要配置 Web 服务器 (特定的 SQL Server)  
  
### <a name="for-microsoft-sql-server-65"></a>对于 Microsoft SQL Server 6.5:  
  
1.  从开始菜单中，依次指向程序，指向 Microsoft SQL Server 6.5、，然后单击 SQL 客户端配置实用工具。  
  
2.  单击高级选项卡。  
  
3.  在服务器框中，键入要连接到使用 TCP/IP 套接字的服务器的名称。  
  
4.  在 DLL 名称框中，选择 TCP/IP 套接字。  
  
5.  单击添加/修改。 指向此服务器的所有数据源现在将都使用 TCP/IP 套接字。  
  
6.  单击完成。  
  
### <a name="for-microsoft-sql-server-70"></a>对于 Microsoft SQL Server 7.0:  
  
1.  从开始菜单，指向程序，指向 Microsoft SQL Server 7.0、，然后单击客户端配置实用工具。  
  
2.  单击常规选项卡。  
  
3.  单击“添加”。  
  
4.  在服务器别名框中输入服务器的别名。 在网络库中，单击 TCP/IP。 在计算机名称框中，输入侦听 TCP/IP 套接字客户端计算机的计算机名称。 在端口号的框中，输入 SQL Server 在其侦听的端口。  
  
5.  单击确定，并且都可然后再次正常退出实用程序。  
  
## <a name="see-also"></a>请参阅  
 [RDS 基础知识](../../../ado/guide/remote-data-service/rds-fundamentals.md)






















