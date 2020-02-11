---
title: 正在连接到 SQL Server （OracleToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to SQL Server,Synchronizing SQL Server Metadata
ms.assetid: 1b2a8059-1829-4904-a82f-9c06de1e245f
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: cd8f0e57554f32d3b02a6e0e98d3a3645d683bac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68266163"
---
# <a name="connecting-to-sql-server-oracletosql"></a>连接到 SQL Server (OracleToSQL)
若要将 Oracle 数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008、2008 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] R2 或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 或2014，你必须连接到这些目标实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的任何一个。 在连接时，SSMA 将获取实例中所有数据库的元数据， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]并在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元数据资源管理器中显示数据库元数据。 SSMA 存储有关您连接到的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的信息，但不存储密码。  
  
你的连接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将保持活动状态，直到你关闭项目。 重新打开项目时，如果想要与服务器[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]建立活动连接，则必须重新连接到。 在将数据库对象加载到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和迁移数据之前，可以脱机工作。  
  
有关实例的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元数据不会自动同步。 相反，若要更新元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]资源管理器中的元数据， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]必须手动更新元数据。 有关详细信息，请参阅本主题[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]后面的 "同步元数据" 一节。  
  
## <a name="required-sql-server-permissions"></a>必需的 SQL Server 权限  
用于连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的帐户需要不同的权限，具体取决于帐户执行的操作：  
  
-   若要将 Oracle 对象[!INCLUDE[tsql](../../includes/tsql-md.md)]转换为语法、更新中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的元数据或将转换后的语法保存到脚本中，该帐户必须有权登录到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的实例。  
  
-   若要将数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]加载到中，该帐户必须是**sysadmin**服务器角色的成员。 这是安装 CLR 程序集所必需的。  
  
-   若要将数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]迁移到，该帐户必须是**sysadmin**服务器角色的成员。 这是运行代理数据迁移[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]包所必需的。  
  
-   若要运行 SSMA 生成的代码，该帐户必须对目标数据库的**ssma_oracle**架构中的所有用户定义函数都具有**Execute**权限。 这些函数提供了 Oracle 系统函数的等效功能，由转换后的对象使用。  
  
如果用于连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的帐户是执行所有迁移任务，则该帐户必须是**sysadmin**服务器角色的成员。  
  
## <a name="establishing-a-sql-server-connection"></a>建立 SQL Server 连接  
在将 Oracle 数据库对象转换为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]语法之前，必须与要将 oracle 数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的实例建立连接。  
  
定义连接属性时，还可以指定要将对象和数据迁移到的数据库。 在连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之后，你可以在 Oracle 架构级别自定义此映射。 有关详细信息，请参阅[将 Oracle 架构映射到 SQL Server 架构 &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-schemas-to-sql-server-schemas-oracletosql.md)。  
  
> [!IMPORTANT]  
> 尝试连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前，请确保的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在运行，并且可以接受连接。  
  
**连接到 SQL Server**  
  
1.  在 "**文件**" 菜单上，选择 "**连接到 SQL Server**"。  
  
    如果以前连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，则命令名称将**重新连接到 SQL Server**。  
  
2.  在 "连接" 对话框中，输入或选择实例的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]名称。  
  
    -   如果要连接到本地计算机上的默认实例，则可以输入**localhost**或点（**.**）。  
  
    -   如果要连接到另一台计算机上的默认实例，请输入计算机的名称。  
  
    -   如果要连接到另一台计算机上的命名实例，请输入计算机名称后跟反斜杠和实例名称，如 MyServer\MyInstance。  
  
3.  如果实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]配置为接受非默认端口上的连接，请在 " [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **服务器端口**" 框中输入用于连接的端口号。 对于的默认实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，默认端口号为1433。 对于命名实例，SSMA 将尝试从[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服务获取端口号。  
  
4.  在 "**数据库**" 框中，输入目标数据库的名称。  
  
    当你重新连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时，此选项不可用。  
  
5.  在 "**身份验证**" 框中，选择要用于连接的身份验证类型。 若要使用当前的 Windows 帐户，请选择 " **Windows 身份验证**"。 若要使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名，请选择 " **SQL Server 身份验证**"，然后提供登录名和密码。  
  
6.  对于安全连接，将添加两个控件，即 "**加密连接**" 和 " **TrustServerCertificate** " 复选框。 只有在选中 "**加密连接**" 时，" **TrustServerCertificate** " 复选框才可见。 选中 "**加密连接**" （true）并取消选中**TrustServerCertificate** （false）后，它将验证 SQL Server SSL 证书。 验证服务器证书是 SSL 握手过程的一部分，这可确保服务器是要连接到的正确服务器。 为了确保这一点，证书必须安装在客户端和服务器端。  
  
7.  单击“连接”  。  
  
**更高版本兼容性**  
  
-   当创建的迁移项目[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "2005" 时，你将能够连接到2008、2012、2014和2016。  
  
-   当创建的迁移项目[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 时，你将能够连接到2012和2014和2016，但你将无法连接到较低版本，即[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005。  
  
-   如果创建的项目 SQL Server 2012， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]你将[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]能够连接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到2012和2014和2016。  
  
||||||||  
|-|-|-|-|-|-|-|  
|**项目类型 Vs 目标服务器版本**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005<br /> （版本：1.x）|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008<br /> （版本：8.x）|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012 <br />（版本： 11. x）|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014 <br />（版本： 12. x）|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 <br />（版本： 13. x）|Azure SQL DB|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005|是|是|是|是|是||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008||是|是|是|是||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012|||是|是|是||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014||||是|是||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016|||||是||
|Azure SQL DB||||||是|
  
> [!IMPORTANT]
> 数据库对象的转换是根据项目类型执行的，而不是按您连接到的的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本执行的。 如果项目为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005，则即使连接到较高版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016），也会按照2005执行转换。  
  
## <a name="synchronizing-sql-server-metadata"></a>同步 SQL Server 元数据  
与数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]有关的元数据不会自动更新。 元数据资源[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]管理器中的元数据是首次连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时或上次手动更新元数据时的元数据的快照。 您可以为所有数据库或任何单个数据库或数据库对象手动更新元数据。  
  
**同步元数据**  
  
1.  确保你已连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
2.  在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "元数据资源管理器" 中，选中要更新的数据库或数据库架构旁边的复选框。  
  
    例如，若要更新所有数据库的元数据，请选中 "**数据库**" 旁边的复选框。  
  
3.  右键单击 "**数据库**"、"数据库" 或 "数据库架构"，然后选择 "**与数据库同步**"。  
  
## <a name="next-step"></a>下一步  
迁移的下一步取决于你的项目需求：  
  
-   若要自定义 Oracle 架构和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库与架构之间的映射，请参阅[将 oracle 架构映射到 SQL Server 架构 &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-schemas-to-sql-server-schemas-oracletosql.md)。  
  
-   若要自定义项目的配置选项，请参阅[设置项目选项 &#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md)。  
  
-   若要自定义源和目标数据类型的映射，请参阅[&#40;OracleToSQL&#41;映射 Oracle 和 SQL Server 数据类型](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)。  
  
-   如果不需要执行这些任务中的任何一种，可以将 Oracle 数据库对象定义转换为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]对象定义。 有关详细信息，请参阅将[Oracle 架构转换 &#40;OracleToSQL&#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md)。  
  
## <a name="see-also"></a>另请参阅  
[将 Oracle 数据库迁移到 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
