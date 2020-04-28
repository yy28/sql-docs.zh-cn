---
title: 在 SQL Server 上安装 SSMA 组件（SybaseToSQL） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 5ad9e12c-2cdb-4dd2-8703-05a23242d19d
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 1fbc3a8f74b21bd5a53bdd874b5c41ef522e29f6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68029007"
---
# <a name="installing-ssma-components-on-sql-server-sybasetosql"></a>在 SQL Server 上安装 SSMA 组件 (SybaseToSQL)
除了安装 SSMA 外，还必须在运行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的计算机上安装组件，才能使用服务器端数据迁移。 这些组件包括支持数据迁移的 SSMA 扩展包和用于启用服务器到服务器连接的 Sybase 提供程序。  
  
## <a name="ssma-for-sybase-extension-pack"></a>用于 Sybase 扩展包的 SSMA  
SSMA 扩展包将数据库、 **sysdb**和**ssmatesterdb_syb**添加到指定的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。 **Sysdb**数据库包含迁移数据所需的表和存储过程。 **Ssmatester_syb**数据库包含架构**ssma_sybase_utilities**，在该架构中创建 ssma 测试器组件使用的对象（表、触发器和视图）。  
  
此外，在将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时，SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]会在服务器端数据迁移引擎用于迁移数据时创建代理作业。  
  
### <a name="installing-the-extension-pack"></a>安装扩展包  
在将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前，你可以随时安装扩展包。  
  
> [!IMPORTANT]  
> 若要安装扩展包，您必须是实例上 sysadmin 服务器角色的成员[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
**安装扩展包**  
  
1.  复制 Sybase 扩展包的 SSMA。*n*。在运行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的计算机上安装 .exe，其中*n*是生成号。  
  
2.  双击 "SSMA for Sybase Extension Pack"。*n*。安装 .exe。  
  
3.  在欢迎页上，单击 "**下一步**"。  
  
4.  在 "最终用户许可协议" 页上，阅读许可协议。 如果同意，请选中 "**我接受许可协议中的条款**" 复选框，然后单击 "**下一步**"。  
  
5.  在 "选择安装类型" 页上，单击 "**典型**"。  
  
6.  在 "准备安装" 页上，单击 "**安装**"。  
  
7.  在 "完成第一步安装" 页上，单击 "**下一**步"。  
  
    此时将显示一个新对话框，您可以在其中选择[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用于安装扩展包的实例。  
  
8.  选择要将 ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库迁移到的实例，然后单击 "**下一步**"。  
  
    默认实例与计算机的名称相同。 命名实例后跟反斜杠和实例名称。  
  
9. 在 "连接参数" 页上，选择身份验证方法，然后单击 "**下一步**"。  
  
    Windows 身份验证将使用您的 Windows 凭据来尝试登录到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果选择[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "身份验证"，则必须[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]输入登录名和密码。  
  
10. 在 "管理服务器" 页上，选择 "**安装实用程序数据库** *n*"，其中*n*是版本号，然后单击 "**下一步**"。  
  
    将创建**sysdb**数据库，并在该数据库中创建存储过程。  
  
    如果已选中 "**安装测试者数据库**" 选项，则将创建**ssmatesterdb_syb**数据库的测试人员。  
  
11. 若要将实用工具安装到的另[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]一个实例，请选择 "**返回到实例**"，然后单击 "**下一步**"。 或者，若要退出向导，请单击 "**退出**"。  
  
### <a name="sql-server-database-objects"></a>SQL Server 数据库对象  
安装扩展包后，将在**sysdb**数据库中看到一个**ssma_syb bcp_migration_packages**表。 你还将看到以下存储过程：  
  
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
  
每次将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时，SSMA 会创建[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理作业。 这些作业**ssma_syb 数据迁移包 {GUID}** 命名，在 "作业" 文件夹的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "代理" [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]节点中可见。  
  
## <a name="sybase-providers"></a>Sybase 提供程序  
将数据从 ASE 迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL azure 时，数据直接在 ASE 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL azure 之间迁移。 它不会经历 SSMA，因为这会降低数据迁移速度。  
  
### <a name="installing-the-sybase-providers"></a>安装 Sybase 提供程序  
以下说明提供了安装 Sybase 提供程序的基本安装步骤。 确切的说明将有所不同，具体取决于 Sybase 安装程序的版本。  
  
> [!IMPORTANT]  
> 在运行安装程序之前，请验证你是否不违反许可协议。  
  
1.  运行 Sybase ASE 安装程序。  
  
2.  选择 "自定义安装"。  
  
3.  在 "功能选择" 页上，选择 ODBC、OLE DB 和 ADO.NET 数据提供程序。  
  
4.  验证所选功能，然后单击 "**完成**" 以安装数据提供程序。  
  
## <a name="see-also"></a>另请参阅  
[为 Sybase 客户端 &#40;SybaseToSQL&#41;安装 SSMA](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[将 Sybase ASE 数据库迁移到 SQL Server-Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
