---
title: 连接到 SQL Server (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Connecting to SQL Server,Synchronizing SQL Server Metadata
ms.assetid: 1b2a8059-1829-4904-a82f-9c06de1e245f
caps.latest.revision: 16
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 3360da5567d1ff1efef7cbac8e235bc508bef3bb
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "40396226"
---
# <a name="connecting-to-sql-server-oracletosql"></a>连接到 SQL Server (OracleToSQL)
将 Oracle 数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005 中， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008年[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008 R2 或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012年或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014 必须连接到其中的任何目标实例的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 SSMA 连接时，获取有关的实例中的所有数据库的元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，并显示数据库中的元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元数据资源管理器。 SSMA 存储信息的哪些实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]相连，但不存储密码。  
  
与连接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]保持活动状态，直到关闭该项目。 当你重新打开该项目时，您必须重新连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]如果想要的活动连接到服务器。 您可以脱机处理之前加载到的数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]并将数据迁移。  
  
有关实例的元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不会自动同步。 相反，若要更新中的元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元数据资源管理器，则必须手动更新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元数据。 有关详细信息，请参阅"正在同步[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元数据"在本主题后面的部分。  
  
## <a name="required-sql-server-permissions"></a>所需的 SQL Server 权限  
用于连接到的帐户[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]需要不同的权限，具体取决于该帐户执行的操作：  
  
-   要转换到的 Oracle 对象[!INCLUDE[tsql](../../includes/tsql-md.md)]语法中，更新元数据，从[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，或将保存到脚本转换后的语法，该帐户必须有权登录到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   若要加载到数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，帐户必须隶属**sysadmin**服务器角色。 这被必需安装 CLR 程序集。  
  
-   若要将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，帐户必须隶属**sysadmin**服务器角色。 这运行所必需[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理数据迁移包。  
  
-   若要运行的代码生成的 SSMA，帐户必须具有**Execute**中的所有用户定义函数的权限**ssma_oracle**目标数据库的架构。 这些函数提供的 Oracle 系统函数的等效的功能，并使用的已转换的对象。  
  
如果用于连接到的帐户[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]是执行所有迁移任务，则必须将帐户的成员**sysadmin**服务器角色。  
  
## <a name="establishing-a-sql-server-connection"></a>建立 SQL Server 连接  
在转换到的 Oracle 数据库对象之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]语法，必须建立的实例的连接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]想要迁移的 Oracle 数据库。  
  
在定义的连接属性时，还可以指定对象和数据将迁移的数据库。 连接到后，您可以自定义此映射 Oracle 架构级别上的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关详细信息，请参阅[映射到 SQL Server 架构的 Oracle 架构&#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-schemas-to-sql-server-schemas-oracletosql.md)。  
  
> [!IMPORTANT]  
> 在尝试连接到之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请确保实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在运行，并且可以接受连接。  
  
**若要连接到 SQL Server**  
  
1.  上**文件**菜单中，选择**连接到 SQL Server**。  
  
    如果你以前连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，命令名称将是**重新连接到 SQL Server**。  
  
2.  在连接对话框中，输入或选择的实例的名称[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
    -   如果要连接到本地计算机上的默认实例，则可以输入**localhost**或句点 (**。**)。  
  
    -   如果要连接到另一台计算机上的默认实例，输入的计算机的名称。  
  
    -   如果要连接到另一台计算机上的命名实例，输入计算机名称后跟反斜杠，然后该实例名称，例如 MyServer\MyInstance。  
  
3.  如果你的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]配置为接受非默认端口上的连接，请输入用于的端口号[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的连接**服务器端口**框。 对于默认实例的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，默认端口号为 1433年。 对于命名实例，SSMA 会尝试获取端口号从[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]浏览器服务。  
  
4.  在中**数据库**框中，输入目标数据库的名称。  
  
    此选项不可用，当重新连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
5.  在中**身份验证**框中，选择要用于连接的身份验证类型。 若要使用当前 Windows 帐户，请选择**Windows 身份验证**。 若要使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名，选择**SQL Server 身份验证**，然后提供登录名和密码。  
  
6.  对于安全的连接，将添加两个控件，**加密连接**并**TrustServerCertificate**复选框。 仅当**加密连接**处于选中状态， **TrustServerCertificate**复选框是否可见。 当**加密连接**已选中 (true) 和**TrustServerCertificate**处于未选中状态 (false)，它将验证 SQL Server SSL 证书。 验证服务器证书是 SSL 握手过程的一部分，这可确保服务器是要连接到的正确服务器。 若要确保这一点，必须在客户端和服务器端上安装证书。  
  
7.  单击 **“连接”**。  
  
**更高版本兼容性**  
  
-   你将能够连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008年并[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012年并[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014年并[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016 时创建的迁移项目[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005年。  
  
-   你将能够连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012年并[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014年和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016 时创建的迁移项目[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008年，但您将无法再即连接到较低版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
-   你将能够连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012年并[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014年和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016 时创建的项目是 SQL Server 2012。  
  
||||||||  
|-|-|-|-|-|-|-|  
|**项目类型与目标服务器版本**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005<br /> (版本： 9.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008<br /> (版本： 10.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 <br />(Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 <br />(Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 <br />(Version:13.x)|Azure SQL DB|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005|用户帐户控制|是|是|是|用户帐户控制||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008||用户帐户控制|是|是|用户帐户控制||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|||用户帐户控制|是|用户帐户控制||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014||||用户帐户控制|用户帐户控制||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016|||||用户帐户控制||
|Azure SQL DB||||||用户帐户控制|
  
> [!IMPORTANT]  
> 根据项目类型，但不是根据版本的数据库对象的转换执行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]连接到。 情况下[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2005年项目中，执行转换为每个[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]即使你已连接到更高版本的 2005年[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008年或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2012年或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014年或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2016年)。  
  
## <a name="synchronizing-sql-server-metadata"></a>同步 SQL Server 元数据  
有关的元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库不会自动更新。 中的元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元数据资源管理器是元数据的快照，首次连接到时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，或上一次你手动更新的元数据。 您可以手动更新所有数据库，或任何单个数据库或数据库对象的元数据。  
  
**同步元数据**  
  
1.  请确保连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
2.  在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元数据资源管理器中，选择数据库旁边的复选框或数据库你想要更新的架构。  
  
    例如，若要更新所有数据库的元数据，请选中框旁边**数据库**。  
  
3.  右键单击**数据库**，或单个数据库或数据库架构，然后选择**与数据库同步**。  
  
## <a name="next-step"></a>下一步  
迁移的下一步取决于您的项目需求：  
  
-   若要自定义 Oracle 架构之间的映射并[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库和架构，请参阅[Oracle 架构映射到 SQL Server 架构&#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-schemas-to-sql-server-schemas-oracletosql.md)。  
  
-   若要自定义项目的配置选项，请参阅[设置项目选项&#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md)。  
  
-   若要自定义源和目标数据类型的映射，请参阅[映射 Oracle 和 SQL Server 数据类型&#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)。  
  
-   如果无需执行任何这些任务，则可以转换到的 Oracle 数据库对象定义[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]对象定义。 有关详细信息，请参阅[转换 Oracle 架构&#40;OracleToSQL&#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md)。  
  
## <a name="see-also"></a>请参阅  
[迁移的 Oracle 数据库移到 SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
