---
title: 在系统管理员被锁定时连接到 SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- sa account
- connecting when locked out [SQL Server]
- locked out [SQL Server]
ms.assetid: c0c0082e-b867-480f-a54b-79f2a94ceb67
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 156a8e765812c14da0888148505311d52c267916
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62782380"
---
# <a name="connect-to-sql-server-when-system-administrators-are-locked-out"></a>在系统管理员被锁定时连接到 SQL Server
  本主题介绍如何以系统管理员身份重新获得对 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的访问权限。 系统管理员可能会由于下列原因之一失去对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的访问权限：  
  
-   作为 sysadmin 固定服务器角色成员的所有登录名都已经被误删除。  
  
-   作为 sysadmin 固定服务器角色成员的所有 Windows 组都已经被误删除。  
  
-   作为 sysadmin 固定服务器角色成员的登录名用于已经离开公司或者无法找到的个人。  
  
-   sa 帐户被禁用或者没有人知道密码。  
  
 可以让您重新获得访问权限的一种方法是重新安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 并将所有数据库附加到新实例。 这种解决方案很耗时，并且若要恢复登录名，可能还需要从备份中还原 master 数据库。 如果 master 数据库的备份较旧，则它可能未包含所有信息。 如果 master 数据库的备份较新，则它可能与前一个实例具有同样的登录名；因此管理员仍将被锁定。  
  
## <a name="resolution"></a>解决方法  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -m **或** -f **选项在单用户模式下启动** 的实例。 计算机的本地 Administrators 组的任何成员都可以随后作为 sysadmin 固定服务器角色的成员连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
> [!NOTE]  
>  在单用户模式下启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例时，请首先停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务。 否则， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理可能会首先连接，并阻止您作为第二个用户连接。  
  
 当你将 **-m** 选项与 **sqlcmd** 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]结合使用时，可以将连接限制为指定的客户端应用程序。 例如， **-m"sqlcmd"** 将连接限制为单个连接，并且该连接必须将自身标识为 **sqlcmd** 客户端程序。 当您正在单用户模式下启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 并且未知的客户端应用程序正在占用这个唯一的可用连接时，使用此选项。 若要通过 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中的查询编辑器进行连接，请使用 **-m"Microsoft SQL Server Management Studio - Query"** 。  
  
> [!IMPORTANT]  
>  不要将此选项作为安全功能使用。 客户端应用程序提供客户端应用程序名称，并且提供假名称来作为连接字符串的一部分。  
  
 有关如何在单用户模式下启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的分步说明，请参阅 [配置服务器启动选项（SQL Server 配置管理器）](scm-services-configure-server-startup-options.md)。  
  
## <a name="step-by-step-instructions"></a>分步说明  
 下面的说明介绍了如何连接到 Windows 8 或更高版本上运行的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 。 对于早期的 SQL Server 或 Windows 版本略有调整。 在作为本地管理员组的成员登录到 Windows 时必须按这些说明操作，假定在计算机上安装了 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。  
  
1.  从“开始”页启动 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 在“视图”  菜单上，选择“已注册的服务器”  。 （如果尚未注册你的服务器，请右键单击“本地服务器组”，指向“任务”，然后单击“注册本地服务器”。    ）  
  
2.  在“已注册的服务器”区域中，右键单击你的服务器，然后单击“SQL Server 配置管理器”  。 这应要求以管理员身份运行的权限，然后打开配置管理器程序。  
  
3.  关闭 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。  
  
4.  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器的左窗格中，选择“SQL Server 服务”  。 在右窗格中，查找 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 （[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的默认实例包括在计算机名称后的 **(MSSQLSERVER)** 。 命名实例显示为大写，名称与在“已注册的服务器”中的名称相同。）右键单击 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例，然后单击“属性”  。  
  
5.  上**启动参数**选项卡上，在**指定启动参数**框中，键入`-m`，然后单击`Add`。 （这是短划线后跟小写字母 m。）  
  
    > [!NOTE]  
    >  对于某些早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，没有“启动参数”  选项卡。在这种情况下，在“高级”选项卡上，双击“启动参数”   。 参数在非常小的窗口中打开。 请注意不要更改任何现有参数。 在最后，添加新参数 `;-m`，然后单击 `OK`。 （这是一个分号，后跟短划线和小写字母 m。）  
  
6.  单击`OK`，右键单击服务器名称，并重新启动的消息，显示后，然后单击**重新启动**。  
  
7.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 重启之后，你的服务器将处于单用户模式。 请确保 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理未在运行。 如果启动，它将占用您唯一的连接。  
  
8.  在 Windows 8 启动屏幕上，右键单击 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 的图标。 在屏幕的底部，选择““以管理员身份运行”  。 （这会将您的管理员凭据传递到 SSMS。）  
  
    > [!NOTE]  
    >  对于 Windows 的早期版本，“以管理员身份运行”选项显示为子菜单  。  
  
     在某些配置中，SSMS 将尝试进行多个连接。 多个连接将失败，因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 处于单用户模式。 可以选择执行以下操作之一。 执行下列操作之一：  
  
    1.  使用 Windows 身份验证（包括您的管理员凭据）与对象资源管理器连接。 依次展开“安全性”和“登录名”，然后双击你自己的登录名   。 上**服务器角色**页上，选择`sysadmin`，然后单击`OK`。  
  
    2.  使用 Windows 身份验证（包括您的管理员凭据）与“查询窗口”连接，而非与对象资源管理器连接。 （如果未与对象资源管理器连接，则只能这样连接）。执行类似以下内容，以添加新的 Windows 身份验证登录名是成员的代码，`sysadmin`固定的服务器角色。 以下示例添加名为 `CONTOSO\PatK`的域用户。  
  
        ```  
        CREATE LOGIN [CONTOSO\PatK] FROM WINDOWS;  
        ALTER SERVER ROLE sysadmin ADD MEMBER [CONTOSO\PatK];  
        ```  
  
    3.  如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在混合身份验证模式下运行，请使用 Windows 身份验证（包括您的管理员凭据）与“查询窗口”连接。 执行类似以下内容，以创建一个新的代码[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的成员身份验证登录名`sysadmin`固定的服务器角色。  
  
        ```  
        CREATE LOGIN TempLogin WITH PASSWORD = '************';  
        ALTER SERVER ROLE sysadmin ADD MEMBER TempLogin;  
        ```  
  
        > [!WARNING]  
        >  使用强密码替换 ************。  
  
    4.  如果你[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在混合身份验证模式，并且你想要重置的密码`sa`帐户，请使用 Windows 身份验证 （其中包括你的管理员凭据） 的查询窗口连接。 更改的密码`sa`帐户使用以下语法。  
  
        ```  
        ALTER LOGIN sa WITH PASSWORD = '************';  
        ```  
  
        > [!WARNING]  
        >  使用强密码替换 ************。  
  
9. 以下步骤现在将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 改回多用户模式。 关闭 SSMS。  
  
10. 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器的左窗格中，选择“SQL Server 服务”  。 在右侧窗格中，右键单击 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例，然后单击“属性”  。  
  
11. 上**启动参数**选项卡上，在**现有参数**框中，选择`-m`，然后单击`Remove`。  
  
    > [!NOTE]  
    >  对于某些早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，没有“启动参数”  选项卡。在这种情况下，在“高级”选项卡上，双击“启动参数”   。 参数在非常小的窗口中打开。 删除`;-m`的前面，添加，然后单击`OK`。  
  
12. 右键单击你的服务器名称，然后单击“重启”  。  
  
 现在您应能与它现在是成员的帐户之一正常连接的`sysadmin`固定的服务器角色。  
  
## <a name="see-also"></a>请参阅  
 [在单用户模式下启动 SQL Server](start-sql-server-in-single-user-mode.md)   
 [数据库引擎服务启动选项](database-engine-service-startup-options.md)  
  
  
