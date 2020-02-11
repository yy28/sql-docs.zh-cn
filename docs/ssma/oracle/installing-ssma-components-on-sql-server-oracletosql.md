---
title: 在 SQL Server 上安装 SSMA 组件（OracleToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 10/01/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Installign the Extension Pack
- SQL Server Database Objects
ms.assetid: 33070e5f-4e39-4b70-ae81-b8af6e4983c5
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 1f0cea859e9465eebefebc061ee51107dc7844aa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "71713313"
---
# <a name="installing-ssma-components-on-sql-server-oracletosql"></a>在 SQL Server 上安装 SSMA 组件（OracleToSQL）

除了安装 SSMA 外，还必须在运行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的计算机上安装组件。 这些组件包括支持数据迁移的 SSMA 扩展包和用于启用服务器到服务器连接的 Oracle 提供程序。  
  
## <a name="ssma-for-oracle-extension-pack"></a>Oracle 扩展包的 SSMA

SSMA 扩展包将**sysdb**和**ssmatesterdb**数据库添加到的指定实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 数据库**sysdb**包含迁移数据所需的表和存储过程，以及用于模拟 Oracle 系统功能的用户定义函数。 **Ssmatesterdb**数据库包含测试人员组件所需的表和过程。  
  
此外，在将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时，SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]会在服务器端数据迁移引擎用于迁移数据时创建代理作业。  
  
### <a name="prerequisites"></a>必备条件

在上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装用于 Oracle 服务器组件的 SSMA 之前，请确保系统满足以下要求：  
  
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]已安装实例。 SSMA 不支持 SQL Server 2008 Express Edition。
  
- 
  [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 或更高版本。  
  
- Oracle 客户端提供程序或用于 Oracle 的 OLE DB 提供程序，以及与要迁移的 Oracle 数据库的连接。 你可以从 Oracle 产品媒体或 Oracle 网站安装提供程序。  
  
- 必须[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在安装过程中运行 Browser 服务。 这用于在安装向导中填充实例的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]列表。 你可以在安装[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]后禁用 Browser 服务。  
  
    > [!NOTE]  
    > 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服务正在运行，但你仍未在安装程序中看到实例列表，则必须解除 UDP 端口1434的阻止。 可以使用 Windows 防火墙暂时取消阻止端口，也可以暂时禁用 Windows 防火墙。 你可能还必须暂时禁用防病毒软件。 请确保在安装后启用防火墙和防病毒软件。  
  
### <a name="installing-the-extension-pack"></a>安装扩展包

在将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前，你可以随时安装扩展包。  
  
> [!IMPORTANT]  
> 若要安装扩展包，您必须是实例上**sysadmin**服务器角色的成员[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
**安装扩展包**
  
1. 如果尚未这样做，请从 SSMA Zip 文件提取所有文件。  
  
    根据你所拥有的 WinZip 版本，可以双击该文件，或者右键单击该文件，然后选择 "**全部提取**" 或 **"在 WinZip 中打开**"。 按照 WinZip 用户界面中的说明提取文件。  
  
2. 复制**Oracle 扩展包的 SSMA。*n*。** 在运行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的计算机上安装 .exe （其中*n*为内部版本号）。  
  
3. 双击 " **SSMA For Oracle Extension Pack"。*n*。安装 .exe**。  
  
4. 在“欢迎”页上，选择“下一步”。********  
  
5. 在 "**最终用户许可协议**" 页上，阅读许可协议。 如果同意，请选中 "**我接受许可协议中的条款**" 复选框，然后选择 "**下一步**"。  
  
6. 在 "**选择安装类型**" 页上，选择 "**典型**"。  
  
7. 在 "**准备安装**" 页上，选择 "**安装**"。  
  
8. 在 "**完成第一步安装**" 页上，选择 "**下一**步"。  
  
    此时将显示一个新对话框，您可以在其中选择[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用于安装扩展包的实例。  
  
9. 选择要将 Oracle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]架构迁移到的实例，然后选择 "**下一步**"。  
  
    默认实例与计算机的名称相同。 命名实例后跟反斜杠和实例名称。  
  
10. 在 "连接" 页上，选择身份验证方法，然后选择 "**下一步**"。  
  
    Windows 身份验证将使用您的 Windows 凭据来尝试登录到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果选择[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "身份验证"，则必须[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]输入登录名和密码。  
  
11. 在下一页上，选择 "**安装实用程序数据库** *n*"，其中*n*是版本号，然后选择 "**下一步**"。  
  
    将创建**sysdb**数据库，并在该数据库中创建用户定义函数和存储过程。  
  
    如果选中了 "**安装测试器数据库**" 选项，则将创建测试**ssmatesterdb**数据库。  
  
12. 若要将实用工具安装到的另[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]一个实例，请选择 **"是**"，然后选择 "**下一步**"，或者单击 "**否**" 以退出向导。  
  
13. 在[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或使用 sqlcmd 实用工具，运行以下脚本以启用 CLR：  
  
    ```
    sp_configure 'clr enabled', 1  
    GO  
    RECONFIGURE  
    GO  
    ```

    如果未启用 CLR，则当 SSMA 连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时，你将收到以下错误：  
  
    SSMA 无法检索扩展包程序集版本信息。 在数据库服务器上重新安装扩展包。  
  
### <a name="sql-server-database-objects"></a>SQL Server 数据库对象  

安装扩展包后， **sysdb**数据库中会出现一个**ssma_oracle bcp_migration_packages**表。

每次将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时，SSMA 会[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]创建代理作业。 这些作业**ssma_oracle 数据迁移包 {GUID}** 命名，在 "作业" 文件夹的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "代理" [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]节点中可见。  
  
## <a name="see-also"></a>另请参阅

[安装 SSMA for Oracle Client &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[将 Oracle 数据库迁移到 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
