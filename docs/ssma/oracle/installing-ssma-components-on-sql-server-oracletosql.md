---
title: "在 SQL Server (OracleToSQL) 上安装 SSMA 组件 |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Installign the Extension Pack
- SQL Server Database Objects
ms.assetid: 33070e5f-4e39-4b70-ae81-b8af6e4983c5
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a363954dd56d20d3fb47d15c6325526bba8cf808
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="installing-ssma-components-on-sql-server-oracletosql"></a>在 SQL Server (OracleToSQL) 上安装 SSMA 组件
除了安装 SSMA，你还必须安装组件正在运行的计算机上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 这些组件包括 SSMA 扩展包，它支持数据迁移和 Oracle 提供程序启用服务器到服务器的连接。  
  
## <a name="ssma-for-oracle-extension-pack"></a>SSMA for Oracle 扩展包  
SSMA 扩展包增加了数据库， **sysdb**和**ssmatesterdb**，到的指定实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 数据库**sysdb**包含表和存储迁移数据，所需的过程和模拟 Oracle 系统函数的用户定义函数。 **Ssmatesterdb**数据库包含的表和所需的测试人员组件的过程。  
  
此外，当你将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，SSMA 创建[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]代理作业时服务器端数据迁移引擎用于将数据迁移。  
  
### <a name="prerequisites"></a>必要條件  
在上安装 Oracle 服务器组件 SSMA 之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，请确保系统满足以下要求：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]安装实例。 SSMA 不支持 SQL Server 2008 Express Edition。  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更高版本。  
  
-   Oracle 客户端提供程序或用于 Oracle 的 OLE DB 访问接口和连接到你想要迁移的 Oracle 数据库。 你可以从 Oracle 产品媒体或 Oracle 网站上安装提供程序。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]浏览器服务必须在安装期间运行。 这用于填充的实例列表[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]安装向导中。 你可以禁用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]后安装的浏览器服务。  
  
    > [!NOTE]  
    > 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]浏览器服务正在运行，但你仍不会看到安装程序中的实例列表，你必须取消阻止 UDP 端口 1434年。 你可以使用 Windows 防火墙暂时取消阻止该端口，或者您可以临时禁用 Windows 防火墙。 你还可能必须暂时禁用防病毒软件。 请确保防火墙和防病毒软件安装后启用。  
  
### <a name="installing-the-extension-pack"></a>安装的扩展包  
你可以安装的扩展包之前迁移到的数据的任何时间[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
> [!IMPORTANT]  
> 若要安装的扩展包，你必须**sysadmin**的实例上的服务器角色[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
**若要安装的扩展包**  
  
1.  如果尚未这样做，则从 SSMA Zip 文件中提取所有文件。  
  
    具体取决于 WinZip 你具有的版本，你可以双击该文件，或右键单击该文件和选择**提取所有**或**在 WinZip 中打开**。 按照 WinZip 用户界面中的说明，以提取文件。  
  
2.  将 SSMA 复制 Oracle 扩展包。*n*.Install.exe，其中 *n* 是到正在运行的计算机的生成号[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
3.  双击 SSMA Oracle 扩展包。*n*.Install.exe。  
  
4.  在欢迎页上，单击**下一步**。  
  
5.  在最终用户许可协议页上，阅读许可协议。 如果同意，请选中**我接受许可协议中的条款**复选框，并依次**下一步**。  
  
6.  在选择安装类型页上，单击**典型**。  
  
7.  在准备安装页面上，单击**安装**。  
  
8.  在已完成安装第一个步骤页上，单击**下一步**。  
  
    将出现新的对话框中，在其中选择的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]扩展包安装。  
  
9. 选择的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]其中你将会迁移 Oracle 架构，然后单击**下一步**。  
  
    默认实例具有相同名称的计算机。 命名的实例将跟反斜杠和实例名称。  
  
10. 在连接页中，选择身份验证方法，然后单击**下一步**。  
  
    Windows 身份验证将使用您的 Windows 凭据来尝试登录到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 如果你选择[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]身份验证，你必须输入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]登录名和密码。  
  
11. 在下一页上，选择**安装实用工具数据库**  *n* ，其中 *n* 是版本号，并依次**下一步**。  
  
    **Sysdb**创建数据库和该数据库中创建的用户定义函数和存储的过程。  
  
    如果**安装测试人员数据库**选中选项测试人员**ssmatesterdb**将创建数据库。  
  
12. 若要安装到另一个实例的实用工具[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，选择**是**，然后单击**下一步**。 或者，若要退出向导，请单击**否**。  
  
13. 在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]或通过使用 sqlcmd 实用工具，运行以下脚本来启用 CLR:  
  
    ```  
    sp_configure 'clr enabled', 1  
    GO  
    RECONFIGURE  
    GO  
    ```  
    如果未启用 CLR，你将收到以下错误，当连接到的 SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]:  
  
    SSMA 无法检索的扩展包的程序集版本信息。 在数据库服务器上重新安装扩展包。  
  
### <a name="sql-server-database-objects"></a>SQL Server 数据库对象  
安装的扩展包后，将会请参阅**ssma_oracle.bcp_migration_packages**表， **ssma_oracle.db_storage**表，和**ssma_oracle.db_error_list**表中**sysdb**数据库。 你还将看到许多存储的过程和中的用户定义函数**ssma_oracle**架构。  
  
你将数据迁移到每次[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，SSMA 创建[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]代理作业。 这些作业将命名为**ssma_oracle 数据迁移包 {GUID}**，并且在中可见[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]代理节点[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]Jobs 文件夹中。  
  
## <a name="see-also"></a>另請參閱  
[安装适用于 Oracle 客户端 &#40; OracleToSQL &#41; SSMA](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[将 Oracle 数据库迁移到 SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  

