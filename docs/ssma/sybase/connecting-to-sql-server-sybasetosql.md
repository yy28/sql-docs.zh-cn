---
title: 连接到 SQL Server (SybaseToSQL) |Microsoft 文档
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
helpviewer_keywords:
- Connecting to SQL Server
ms.assetid: dd368a1a-45b0-40e9-b4d3-5cdb48c26606
caps.latest.revision: 15
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 64d7dd2cf9ac9a0a83e35a8d6a0e4a7abc81eaff
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2018
ms.locfileid: "34778683"
---
# <a name="connecting-to-sql-server-sybasetosql"></a>连接到 SQL Server (SybaseToSQL)
若要 Sybase 自适应 Server Enterprise (ASE) 将数据库迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，你必须连接到的目标实例的任何[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 SSMA 连接时，获取有关的实例中的所有数据库的元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]并显示在数据库元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]元数据资源管理器。 SSMA 存储的哪个实例有关的信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]已连接，但不会存储密码。  
  
与连接[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]将保持活动状态，直到关闭该项目。 当你重新打开项目时，你必须重新连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]如果想与服务器的活动连接。 您可以离线工作之前加载到的数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]并迁移数据。  
  
元数据的实例的有关[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]不会自动同步。 相反，如果你想要更新的元数据中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]元数据资源管理器，你必须手动更新[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]元数据中所述"正在同步[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]元数据"本主题中后面的部分。  
  
## <a name="required-sql-server-permissions"></a>所需的 SQL Server 权限  
用于连接到的帐户[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]需要不同的权限，具体取决于该帐户通过执行的操作。  
  
-   要转换到的 ASE 对象[!INCLUDE[tsql](../../includes/tsql_md.md)]语法中，以更新元数据从[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，若要将已转换的语法保存到脚本中，帐户必须有权登录到的实例或[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
-   若要加载到的数据库对象[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，最小权限要求是中的成员身份**db_owner**目标数据库中的数据库角色。  
  
-   若要将数据迁移到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，该帐户应是成员的**sysadmin**服务器角色。 运行时需要此[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]代理数据迁移包。  
  
-   若要运行的代码生成的 SSMA，帐户必须具有**执行**权限中的所有用户定义函数**ssma_syb**架构**sysdb**数据库。 这些函数提供等效的功能的 ASE 系统函数，并使用的已转换的对象。  
  
如果用于连接到的帐户[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]是若要执行所有迁移任务，则必须将帐户的成员**sysadmin**服务器角色。  
  
## <a name="establishing-a-sql-server-connection"></a>建立 SQL Server 连接  
在转换到的 ASE 数据库对象之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]语法，必须建立连接到的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]想要迁移或多个 ASE 数据库。  
  
在定义的连接属性时，你还指定对象和数据将迁移的数据库。 连接到后，你可以自定义此映射在 ASE 架构级别[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 有关详细信息，请参阅[映射 Sybase ASE 架构写入 SQL Server 架构&#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)。  
  
> [!IMPORTANT]  
> 尝试连接到之前[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，请确保实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]正在运行并且可以接受连接。  
  
**若要连接到 SQL Server**  
  
1.  上**文件**菜单上，选择**连接到 SQL Server**。  
  
    如果你以前连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，命令名称将**重新连接到 SQL Server**。  
  
2.  在连接对话框中，输入或选择的实例的名称[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
    -   如果你要连接到本地计算机上的默认实例，则可以输入**localhost**或句点 (**。**)。  
  
    -   如果你要连接到另一台计算机上的默认实例，输入的计算机的名称。  
  
    -   如果你要连接到另一台计算机上的命名实例，输入计算机名称后跟反斜杠，然后选择实例名称，如 MyServer\MyInstance。  
  
3.  如果你的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]配置为接受非默认端口上的连接，请输入端口号用于[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]中的连接**服务器端口**框。 对于默认实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，默认端口号为 1433年。 对于命名实例，SSMA 将尝试获取中的端口号[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]浏览器服务。  
  
4.  在**数据库**框中，输入目标数据库的名称。  
  
    此选项不可用，当重新连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
5.  在**身份验证**框中，选择要用于连接的身份验证类型。 若要使用当前的 Windows 帐户，请选择**Windows 身份验证**。 若要使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]登录名选择**SQL Server 身份验证**，然后提供登录名和密码。  
  
6.  对于安全的连接，将添加两个控件，**加密连接**和**TrustServerCertificate**复选框。 仅当**加密连接**已选中， **TrustServerCertificate**复选框是可见的。 当**加密连接**(true) 检查和**TrustServerCertificate**处于未选中状态 (false)，它将验证 SQL Server SSL 证书。 验证服务器证书是 SSL 握手过程的一部分，这可确保服务器是要连接到的正确服务器。 若要确保这一点，必须在客户端上以及在服务器端中安装证书。  
  
7.  单击 **“连接”**。  
  
**更高版本兼容性**  
  
-   你将能够连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2008年和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2012年和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2014年和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2016 时创建的迁移项目[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2005年。  
  
-   你将能够连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2012年和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2014年和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2016 时创建的迁移项目[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2008年但不是会能够即连接到较低版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005.  
  
-   你将能够仅连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2012年和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2014年和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2016 时创建的项目是 SQL Server 2012。  
  
-   更高版本兼容性不是有效的 SQL Azure。  
  
||||||||
|-|-|-|-|-|-|-|
|**项目类型与目标服务器版本**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005<br /> (版本： 9.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008<br /> (版本： 10.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 <br />(Version:11.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 <br />(Version:12.x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 <br />(Version:13.x)|SQL Azure|
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005|是|是|是|是|是||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008||是|是|是|是||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012|||是|是|是||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014||||是|是|| 
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016|||||是||  
|SQL Azure||||||是|  
  
> [!IMPORTANT]  
> 根据项目类型，但不是根据版本的数据库对象的转换执行[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]你连接到。 情况下[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2005年项目转换执行按照[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2005 即使你已连接到更高版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]([!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008年或[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2012年或[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2014年或[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]2016年)  
  
## <a name="reconnecting-to-sql-server"></a>重新连接到 SQL Server  
与连接[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]将保持活动状态，直到关闭该项目。 当你重新打开项目时，你必须重新连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]如果想与服务器的活动连接。 可以更新元数据，将数据库对象加载到前脱机工作[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，并迁移数据。  
  
重新连接到的过程[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]建立的连接的过程相同。  
  
## <a name="synchronizing-sql-server-metadata"></a>SQL Server 元数据同步  
有关的元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库不会自动更新。 中的元数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]元数据资源管理器是元数据的快照，首次连接到时[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，或上一次你手动更新的元数据。 你可以手动更新所有数据库，或任何单个数据库或数据库对象的元数据。  
  
**若要同步元数据**  
  
1.  请确保你已连接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。  
  
2.  在[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]元数据资源管理器中，选择数据库旁边的复选框或数据库你想要更新的架构。  
  
    例如，若要更新所有数据库的元数据，请选中框旁边**数据库**。  
  
3.  右键单击数据库或单个数据库或数据库架构，然后选择**与数据库的同步**。  
  
## <a name="next-step"></a>下一步  
迁移的下一步取决于您的项目需求：  
  
-   如果你想要自定义 ASE 数据库和架构之间的映射和[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库和架构，请参阅[映射 Sybase ASE 架构写入 SQL Server 架构&#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)。  
  
-   如果你想要自定义项目的配置选项，请参阅[设置项目选项&#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)。  
  
-   如果你希望的自定义的源和目标数据类型映射，请参阅[映射 Sybase ASE 和 SQL Server 数据类型&#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)。  
  
-   如果不需要执行下列任一操作，你可以将转换到的 Sybase ASE 数据库对象定义[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]对象定义。 有关详细信息，请参阅[转换 Sybase ASE 数据库对象&#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)。  
  
## <a name="see-also"></a>请参阅  
[将 Sybase ASE 数据库迁移到 SQL Server 的 Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
