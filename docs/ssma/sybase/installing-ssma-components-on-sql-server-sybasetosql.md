---
title: 在 SQL Server (SybaseToSQL) 上安装 SSMA 组件 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 5ad9e12c-2cdb-4dd2-8703-05a23242d19d
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 17d9068497072660fd48888a2b4652dcb46815cf
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2018
ms.locfileid: "34779253"
---
# <a name="installing-ssma-components-on-sql-server-sybasetosql"></a>在 SQL Server (SybaseToSQL) 上安装 SSMA 组件
除了安装之外 SSMA，使用服务器端数据迁移，你还必须安装组件正在运行的计算机上[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 这些组件包括 SSMA 扩展包，它支持数据迁移和 Sybase 提供程序启用服务器到服务器的连接。  
  
## <a name="ssma-for-sybase-extension-pack"></a>SSMA for Sybase 扩展包  
SSMA 扩展包增加了数据库， **sysdb**和**ssmatesterdb_syb**，到的指定实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 **Sysdb**数据库包含的表和所需迁移数据的存储的过程。 **Ssmatester_syb**数据库包含架构**ssma_sybase_utilities**，在其中创建 SSMA 测试人员组件使用的对象 （表、 触发器视图）。  
  
此外，当你将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，SSMA 创建[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]代理作业时服务器端数据迁移引擎用于将数据迁移。  
  
### <a name="installing-the-extension-pack"></a>安装的扩展包  
你可以安装的扩展包之前迁移到的数据的任何时间[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
> [!IMPORTANT]  
> 若要安装的扩展包，你必须是 sysadmin 服务器角色的实例上的成员[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
**若要安装的扩展包**  
  
1.  将 SSMA 复制 Sybase 扩展包。*n*。Install.exe，其中*n*是到正在运行的计算机的生成号[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
2.  双击 SSMA Sybase 扩展包。*n*。Install.exe。  
  
3.  在欢迎页上，单击**下一步**。  
  
4.  在最终用户许可协议页上，阅读许可协议。 如果同意，请选中**我接受许可协议中的条款**复选框，并依次**下一步**。  
  
5.  在选择安装类型页上，单击**典型**。  
  
6.  在准备安装页面上，单击**安装**。  
  
7.  在已完成安装第一个步骤页上，单击**下一步**。  
  
    将出现新的对话框中，在其中选择的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]扩展包安装。  
  
8.  选择的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]其中你将会迁移 ASE 数据库，然后单击**下一步**。  
  
    默认实例具有相同名称的计算机。 命名的实例将跟反斜杠和实例名称。  
  
9. 在连接参数页中，选择身份验证方法，然后单击**下一步**。  
  
    Windows 身份验证将使用您的 Windows 凭据来尝试登录到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 如果你选择[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]身份验证，你必须输入[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]登录名和密码。  
  
10. 在管理服务器页中，选择**安装实用工具数据库** *n*，其中*n*是版本号，并依次**下一步**。  
  
    **Sysdb**会创建数据库并在该数据库中创建的存储的过程。  
  
    如果**安装测试人员数据库**选中选项测试人员**ssmatesterdb_syb**将创建数据库。  
  
11. 若要安装到另一个实例的实用工具[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，选择**返回到实例**，然后单击**下一步**。 或者，若要退出向导，请单击**退出**。  
  
### <a name="sql-server-database-objects"></a>SQL Server 数据库对象  
安装的扩展包后，将会请参阅**ssma_syb.bcp_migration_packages**表中**sysdb**数据库。 你将看到以下存储的过程：  
  
-   **bcp_clean_migration_data**  
  
-   **bcp_ensure_message_table**  
  
-   **bcp_insert_new_message**  
  
-   **bcp_post_process**  
  
-   **bcp_read_new_migration_messages**  
  
-   **bcp_save_migration_package**  
  
-   **bcp_smart_truncate**  
  
-   **bcp_start_migration_process**  
  
-   **get_jobstep_info**  
  
-   **stop_agent_process**  
  
你将数据迁移到每次[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，SSMA 创建[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]代理作业。 这些作业将命名为**ssma_syb 数据迁移包 {GUID}**，并且在中可见[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]代理节点[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]Jobs 文件夹中。  
  
## <a name="sybase-providers"></a>Sybase 提供程序  
当你将数据从迁移到的 ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SQL Azure，直接在 ASE 之间迁移数据和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SQL Azure。 它将不会通过 SSMA 因为这会降低数据迁移。  
  
### <a name="installing-the-sybase-providers"></a>安装的 Sybase 提供程序  
以下说明为安装 Sybase 提供程序提供的基本安装步骤。 确切的说明将根据 Sybase 安装程序的版本而有所不同。  
  
> [!IMPORTANT]  
> 运行安装程序之前，请验证未违反您的许可协议。  
  
1.  运行 Sybase ASE 安装程序。  
  
2.  选择自定义安装。  
  
3.  在功能选择页中，选择 ODBC、 OLE DB 和 ADO.NET 数据提供程序。  
  
4.  验证所选的功能，然后单击**完成**安装数据提供程序。  
  
## <a name="see-also"></a>请参阅  
[Sybase 客户端安装 SSMA &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[将 Sybase ASE 数据库迁移到 SQL Server 的 Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
