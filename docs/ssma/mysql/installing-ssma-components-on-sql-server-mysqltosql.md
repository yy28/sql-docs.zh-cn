---
title: SQL Server (MySQLToSql) 上安装 SSMA 组件 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- SSMA extension pack, Installation
ms.assetid: 6772d0c5-258f-4d7b-afb0-b5f810e71af1
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 1f80198787dd85d8f0c65e9881925641f9f081e5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63233036"
---
# <a name="installing-ssma-components-on-sql-server-mysqltosql"></a>在 SQL Server 上安装 SSMA 组件 (MySQLToSql)
除了安装 SSMA，您还必须安装组件正在运行的计算机上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 这些组件包括 SSMA 扩展包，它支持数据迁移和 MySQL 提供程序以启用服务器到服务器的连接。  
  
## <a name="ssma-for-mysql-extension-pack"></a>SSMA for MySQL 扩展包  
SSMA 扩展包添加了一个数据库， **sysdb**，为指定的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 此数据库包含的表和数据迁移所需的存储的过程。  
  
此外，当你将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，SSMA 创建[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理作业，当服务器端数据迁移引擎用于将数据迁移。  
  
### <a name="prerequisites"></a>先决条件  
在上安装 SSMA for MySQL 服务器组件之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请确保计算机满足以下要求：  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更高版本。  
  
-   MySQL 客户端提供程序和连接到你想要迁移的 MySQL 数据库中。 可以从 MySQL 产品媒体或 MySQL 网站上安装提供程序。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]浏览器服务必须在安装过程中运行。 这用于填充列表的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装向导中。 您可以禁用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]后安装的浏览器服务。  
  
    > [!NOTE]  
    > 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]浏览器服务正在运行，但仍未看到安装程序中实例的列表，必须取消阻止 UDP 端口 1434年。 可以使用 Windows 防火墙以便暂时取消阻止端口，或您可以临时禁用 Windows 防火墙。 您可能还需要暂时禁用防病毒软件。 请确保防火墙和防病毒软件安装后启用。  
  
### <a name="installing-the-extension-pack"></a>安装扩展包  
可以安装的扩展包前迁移到的数据的任何时间[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
> [!IMPORTANT]  
> 若要安装的扩展包，您必须**sysadmin**服务器角色的实例上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
**若要安装的扩展包**  
  
1.  复制 SSMA for MySQL 扩展包。*n*。Install.exe，其中*n*是正在运行的计算机的生成号[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
2.  双击 SSMA for MySQL 扩展包。*n*。Install.exe。  
  
3.  在欢迎对话框框中，单击**下一步**。  
  
4.  在最终用户许可协议对话框中，阅读许可协议。 如果同意，请选择**我接受许可协议中条款**复选框，然后依次**下一步**。  
  
5.  在选择安装类型对话框中，单击**典型**。  
  
6.  在已准备好安装对话框的上，单击**安装**。  
  
7.  在已完成安装第一个步骤对话框中，单击**下一步**。  
  
    将出现一个新的对话框，在其中选择的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]扩展包安装。  
  
8.  选择的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您将会迁移 MySQL 架构，然后单击**下一步**。  
  
    默认实例具有相同名称的计算机。 命名的实例将跟一个反斜杠和实例名称。  
  
9. 在连接对话框中，选择身份验证方法，然后单击**下一步**。  
  
    Windows 身份验证将使用你的 Windows 凭据来尝试登录到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果选择[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证，必须输入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名和密码。  
  
10. 在下一步对话框中，选择**安装实用程序数据库** *n*，其中*n*是否的版本号，然后单击**下一步**。  
  
    **Sysdb**数据库创建的表，该数据库中创建所需的数据迁移 （使用服务器端数据迁移引擎） 的存储的过程。  
  
11. 若要安装到另一个实例的实用工具[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，选择**是**，然后单击**下一步**。 若要退出向导，请单击**否**。  
  
## <a name="see-also"></a>请参阅  
[安装 SSMA for MySQL 客户端&#40;MySQLToSQL&#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[迁移 MySQL 数据库移到 SQL Server-Azure SQL 数据库&#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
