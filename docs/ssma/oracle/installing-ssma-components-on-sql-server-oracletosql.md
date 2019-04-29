---
title: SQL Server (OracleToSQL) 上安装 SSMA 组件 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Installign the Extension Pack
- SQL Server Database Objects
ms.assetid: 33070e5f-4e39-4b70-ae81-b8af6e4983c5
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 2041901a851ca755b1079535ccbf763472ec7bc4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63055667"
---
# <a name="installing-ssma-components-on-sql-server-oracletosql"></a>在 SQL Server 上安装 SSMA 组件 (OracleToSQL)
除了安装 SSMA，您还必须安装组件正在运行的计算机上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 这些组件包括 SSMA 扩展包，它支持数据迁移和 Oracle 提供程序以启用服务器到服务器的连接。  
  
## <a name="ssma-for-oracle-extension-pack"></a>SSMA for Oracle 扩展包  
SSMA 扩展包添加了数据库， **sysdb**并**ssmatesterdb**，为指定的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 数据库**sysdb**包含表和存储的过程所需迁移数据，以及模拟 Oracle 系统函数的用户定义函数。 **Ssmatesterdb**数据库包含的表和所需的测试人员组件的过程。  
  
此外，当你将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，SSMA 创建[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理作业时服务器端数据迁移引擎用于将数据迁移。  
  
### <a name="prerequisites"></a>先决条件  
在上安装 SSMA for Oracle 服务器组件之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请确保系统满足以下要求：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装实例。 SSMA 不支持 SQL Server 2008 Express Edition。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更高版本。  
  
-   Oracle 客户端提供程序或 Oracle、 OLE DB 访问接口和连接到你想要迁移的 Oracle 数据库。 可以从 Oracle 产品媒体或 Oracle 网站上安装提供程序。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]浏览器服务必须在安装过程中运行。 这用于填充列表的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装向导中。 您可以禁用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]后安装的浏览器服务。  
  
    > [!NOTE]  
    > 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]浏览器服务正在运行，但仍未看到安装程序中实例的列表，必须取消阻止 UDP 端口 1434年。 可以使用 Windows 防火墙以便暂时取消阻止端口，或您可以临时禁用 Windows 防火墙。 您可能还需要暂时禁用防病毒软件。 请确保防火墙和防病毒软件安装后启用。  
  
### <a name="installing-the-extension-pack"></a>安装扩展包  
可以安装的扩展包前迁移到的数据的任何时间[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
> [!IMPORTANT]  
> 若要安装的扩展包，您必须**sysadmin**服务器角色的实例上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
**若要安装的扩展包**  
  
1.  如果尚未这样做，请从 SSMA Zip 文件中提取所有文件。  
  
    根据您具有的 WinZip 的版本，可以双击该文件，或右键单击该文件，并选择**全部提取**或**WinZip 中打开**。 按照 WinZip 用户界面中的说明以提取文件。  
  
2.  复制 SSMA for Oracle 扩展包。*n*。Install.exe，其中*n*是正在运行的计算机的生成号[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
3.  双击 SSMA for Oracle 扩展包。*n*。Install.exe。  
  
4.  在欢迎页上，单击**下一步**。  
  
5.  在最终用户许可协议页上，阅读许可协议。 如果同意，请选择**我接受许可协议中条款**复选框，然后依次**下一步**。  
  
6.  在选择安装类型页上单击**典型**。  
  
7.  在已准备好安装页上，单击**安装**。  
  
8.  在已完成安装第一个步骤页上，单击**下一步**。  
  
    将出现一个新的对话框，在其中选择的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]扩展包安装。  
  
9. 选择的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您将会迁移 Oracle 架构，然后单击**下一步**。  
  
    默认实例具有相同名称的计算机。 命名的实例将跟一个反斜杠和实例名称。  
  
10. 在连接页面上选择的身份验证方法，然后单击**下一步**。  
  
    Windows 身份验证将使用你的 Windows 凭据来尝试登录到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果选择[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证，必须输入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名和密码。  
  
11. 在下一页上，选择**安装实用程序数据库** *n*，其中*n*是否的版本号，然后单击**下一步**。  
  
    **Sysdb**创建数据库并在该数据库中创建的用户定义的函数和存储的过程。  
  
    如果**安装的测试人员数据库**选项处于选中状态的测试人员**ssmatesterdb**将创建数据库。  
  
12. 若要安装到另一个实例的实用工具[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，选择**是**，然后单击**下一步**。 若要退出向导，请单击**否**。  
  
13. 在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或通过使用 sqlcmd 实用工具，运行以下脚本来启用 CLR:  
  
    ```  
    sp_configure 'clr enabled', 1  
    GO  
    RECONFIGURE  
    GO  
    ```  
    如果未启用 CLR，您将收到以下错误，当连接到的 SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
    SSMA 检索不到扩展包程序集版本信息。 数据库服务器上重新安装扩展包。  
  
### <a name="sql-server-database-objects"></a>SQL Server 数据库对象  
安装扩展包后，将会，请参阅**ssma_oracle.bcp_migration_packages**表中， **ssma_oracle.db_storage**表中，和一个**ssma_oracle.db_error_list**表中**sysdb**数据库。 您还会看到许多存储的过程和中的用户定义函数**ssma_oracle**架构。  
  
你将数据迁移到每次[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，SSMA 创建[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理作业。 这些作业将命名为**ssma_oracle 数据迁移包 {GUID}**，而在中可见[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理节点[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]Jobs 文件夹中。  
  
## <a name="see-also"></a>请参阅  
[安装 SSMA for Oracle 客户端&#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[迁移的 Oracle 数据库移到 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
