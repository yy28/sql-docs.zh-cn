---
title: 在 SQL Server (MySQLToSql) 上安装 SSMA 组件 |Microsoft 文档
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- SSMA extension pack, Installation
ms.assetid: 6772d0c5-258f-4d7b-afb0-b5f810e71af1
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 06c63c033e8c10fcb10bd0c25f868504f43774dd
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="installing-ssma-components-on-sql-server-mysqltosql"></a>在 SQL Server (MySQLToSql) 上安装 SSMA 组件
除了安装 SSMA，你还必须安装组件正在运行的计算机上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 这些组件包括 SSMA 扩展包，它支持数据迁移和 MySQL 提供程序以启用服务器到服务器的连接。  
  
## <a name="ssma-for-mysql-extension-pack"></a>SSMA for MySQL 扩展包  
SSMA 扩展包增加了一个数据库， **sysdb**，到的指定实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 此数据库包含的表和所需迁移数据的存储的过程。  
  
此外，当你将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，SSMA 创建[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]代理作业，当服务器端数据迁移引擎用于将数据迁移。  
  
### <a name="prerequisites"></a>必要條件  
在上安装 MySQL 服务器组件 SSMA 之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，请确保计算机满足以下要求：  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更高版本。  
  
-   MySQL 客户端提供程序，并连接到你想要迁移的 MySQL 数据库中。 你可以从 MySQL 产品媒体或 MySQL 网站安装提供程序。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]浏览器服务必须在安装期间运行。 这用于填充的实例列表[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]安装向导中。 你可以禁用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]后安装的浏览器服务。  
  
    > [!NOTE]  
    > 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]浏览器服务正在运行，但你仍不会看到安装程序中的实例列表，你必须取消阻止 UDP 端口 1434年。 你可以使用 Windows 防火墙暂时取消阻止该端口，或者您可以临时禁用 Windows 防火墙。 你还可能必须暂时禁用防病毒软件。 请确保防火墙和防病毒软件安装后启用。  
  
### <a name="installing-the-extension-pack"></a>安装的扩展包  
你可以安装的扩展包之前迁移到的数据的任何时间[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
> [!IMPORTANT]  
> 若要安装的扩展包，你必须**sysadmin**的实例上的服务器角色[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
**若要安装的扩展包**  
  
1.  将 SSMA 复制 MySQL 扩展包。*n*。Install.exe，其中*n*是到正在运行的计算机的生成号[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
2.  双击 SSMA MySQL 扩展包。*n*。Install.exe。  
  
3.  在欢迎对话框上单击**下一步**。  
  
4.  在最终用户许可协议的对话框中，阅读许可协议。 如果同意，请选中**我接受许可协议中的条款**复选框，并依次**下一步**。  
  
5.  在选择安装类型对话框中，单击**典型**。  
  
6.  在已准备好安装对话框中，单击**安装**。  
  
7.  在已完成第一次安装步骤对话框中，单击**下一步**。  
  
    将出现新的对话框中，在其中选择的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]扩展包安装。  
  
8.  选择的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]其中你将会迁移 MySQL 架构，然后单击**下一步**。  
  
    默认实例具有相同名称的计算机。 命名的实例将跟反斜杠和实例名称。  
  
9. 在连接对话框中，选择身份验证方法，然后单击**下一步**。  
  
    Windows 身份验证将使用您的 Windows 凭据来尝试登录到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 如果你选择[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]身份验证，你必须输入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]登录名和密码。  
  
10. 在下一步的对话框中，选择**安装实用工具数据库** *n*，其中*n*是版本号，并依次**下一步**。  
  
    **Sysdb**与表中创建数据库和数据迁移 （使用服务器端数据迁移引擎） 所需的存储的过程创建该数据库中。  
  
11. 若要安装到另一个实例的实用工具[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，选择**是**，然后单击**下一步**。 或者，若要退出向导，请单击**否**。  
  
## <a name="see-also"></a>另请参阅  
[安装 MySQL 客户端的 SSMA &#40;MySQLToSQL&#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[迁移的 MySQL 数据库移到 SQL Server 的 Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
