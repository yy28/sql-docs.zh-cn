---
title: SQL Server (SybaseToSQL) 上安装 SSMA 组件 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 5ad9e12c-2cdb-4dd2-8703-05a23242d19d
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 6121c75390e7493052a16b2e898eac69283e41ec
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63294573"
---
# <a name="installing-ssma-components-on-sql-server-sybasetosql"></a>在 SQL Server 上安装 SSMA 组件 (SybaseToSQL)
除了安装 SSMA for 使用服务器端数据迁移，你还必须安装组件正在运行的计算机上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 这些组件包括 SSMA 扩展包，它支持数据迁移和 Sybase 提供程序以启用服务器到服务器的连接。  
  
## <a name="ssma-for-sybase-extension-pack"></a>SSMA for Sybase 扩展包  
SSMA 扩展包添加了数据库， **sysdb**并**ssmatesterdb_syb**，为指定的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 **Sysdb**数据库包含的表和数据迁移所需的存储的过程。 **Ssmatester_syb**数据库包含的架构**ssma_sybase_utilities**，在其中创建 SSMA 测试器组件使用的对象 （表、 触发器、 视图）。  
  
此外，当你将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，SSMA 创建[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理作业时服务器端数据迁移引擎用于将数据迁移。  
  
### <a name="installing-the-extension-pack"></a>安装扩展包  
可以安装的扩展包前迁移到的数据的任何时间[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
> [!IMPORTANT]  
> 若要安装的扩展包，您必须是 sysadmin 服务器角色的实例上的成员[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
**若要安装的扩展包**  
  
1.  复制 SSMA for Sybase 扩展包。*n*。Install.exe，其中*n*是正在运行的计算机的生成号[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
2.  双击 SSMA for Sybase 扩展包。*n*。Install.exe。  
  
3.  在欢迎页上，单击**下一步**。  
  
4.  在最终用户许可协议页上，阅读许可协议。 如果同意，请选择**我接受许可协议中条款**复选框，然后依次**下一步**。  
  
5.  在选择安装类型页上单击**典型**。  
  
6.  在已准备好安装页上，单击**安装**。  
  
7.  在已完成安装第一个步骤页上，单击**下一步**。  
  
    将出现一个新的对话框，在其中选择的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]扩展包安装。  
  
8.  选择的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您将是 ASE 数据库迁移，然后单击**下一步**。  
  
    默认实例具有相同名称的计算机。 命名的实例将跟一个反斜杠和实例名称。  
  
9. 在连接参数页上，选择身份验证方法，然后单击**下一步**。  
  
    Windows 身份验证将使用你的 Windows 凭据来尝试登录到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果选择[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证，必须输入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名和密码。  
  
10. 在管理服务器页上选择**安装实用程序数据库** *n*，其中*n*是否的版本号，然后单击**下一步**。  
  
    **Sysdb**创建数据库并在该数据库中创建存储的过程。  
  
    如果**安装的测试人员数据库**选项处于选中状态的测试人员**ssmatesterdb_syb**将创建数据库。  
  
11. 若要安装到另一个实例的实用工具[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，选择**返回到实例**，然后单击**下一步**。 若要退出向导，请单击**退出**。  
  
### <a name="sql-server-database-objects"></a>SQL Server 数据库对象  
安装扩展包后，将会，请参阅**ssma_syb.bcp_migration_packages**表中**sysdb**数据库。 你将看到以下存储的过程：  
  
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
  
你将数据迁移到每次[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，SSMA 创建[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理作业。 这些作业将命名为**ssma_syb 数据迁移包 {GUID}** ，而在中可见[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理节点[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]Jobs 文件夹中。  
  
## <a name="sybase-providers"></a>Sybase 提供程序  
从 ASE 到迁移数据时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SQL Azure，直接在 ASE 之间迁移数据和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SQL Azure。 它不会通过 SSMA 因为这将会减慢数据迁移。  
  
### <a name="installing-the-sybase-providers"></a>安装的 Sybase 提供程序  
以下说明安装 Sybase 提供程序提供的基本安装步骤。 确切说明 Sybase 安装程序的版本而异。  
  
> [!IMPORTANT]  
> 在运行安装程序之前，验证没有违反许可协议。  
  
1.  运行 Sybase ASE 安装程序。  
  
2.  选择自定义安装程序。  
  
3.  在功能选择页中，选择 ODBC、 OLE DB 和 ADO.NET 数据提供程序。  
  
4.  验证所选的功能，然后单击**完成**安装数据提供程序。  
  
## <a name="see-also"></a>请参阅  
[安装 SSMA for Sybase 客户端&#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[将 Sybase ASE 数据库迁移到 SQL Server-Azure SQL 数据库&#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
