---
title: 配置 IIS 以实现 Web 同步 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- IIS server configuration [SQL Server replication]
- websync.log
- Web synchronization, IIS servers
ms.assetid: d651186e-c9ca-4864-a444-2cd6943b8e35
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a5c3b456fa650cff94d0b5809c37f7ceca8b1b71
ms.sourcegitcommit: 961c56bb78ff46ae6eb1a2cc5d2b1262ddf7a4fa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74706666"
---
# <a name="configure-iis-for-web-synchronization"></a>配置 IIS 以实现 Web 同步
  本主题中的过程是为合并复制配置 Web 同步的第二个步骤。 应在为 Web 同步启用发布后执行此步骤。 有关配置过程的概述，请参阅 [“配置 Web 同步”](configure-web-synchronization.md)。 完成本主题中的过程后，请继续执行第三个步骤“配置订阅以使用 Web 同步”。 下列主题中将介绍第三个步骤：  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]：[如何配置订阅以使用 Web \(同步 SQL Server Management Studio\) ](https://msdn.microsoft.com/library/ms345214.aspx)  
  
-   复制 [!INCLUDE[tsql](../../includes/tsql-md.md)] 编程： [如何配置订阅以使用 Web 同步（复制 Transact-SQL 编程）](https://msdn.microsoft.com/library/ms345206.aspx)  
  
-   RMO： [如何配置订阅以使用 Web 同步（RMO 编程）](https://msdn.microsoft.com/library/ms345207.aspx)  
  
 Web 同步使用运行 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS) 的计算机，使请求订阅与合并发布同步。 支持 IIS 5.0、6.0 和 7.0 版。 IIS 版本 7.0 不支持配置 Web 同步向导。  
  
> [!IMPORTANT]  
>  请确保您的应用程序仅使用 [!INCLUDE[dnprdnlong](../../includes/dnprdnlong-md.md)] 或更高版本，并且 IIS 服务器上没有安装 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 的较早版本。 较早版本的 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 可能导致错误。 这些错误包括以下内容：“Web 同步期间出现的消息的格式无效。 请确保在 Web 服务器上正确配置了复制组件”。  
  
> [!CAUTION]  
>  不要同时使用 WebSync 和备用快照文件夹位置。  
  
 若要使用 Web 同步，必须通过完成以下步骤来配置 IIS。 本主题对每个步骤都进行了详细说明。  
  
1.  配置安全套接字层 (SSL)。 IIS 和所有订阅服务器之间的通信需要 SSL。  
  
2.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安装向导在运行 IIS 的计算机上安装连接组件。 如果计划使用步骤 3 中提及的配置 Web 同步向导，那么还必须在运行 IIS 的计算机中安装 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。  
  
3.  为 Web 同步配置正在运行 IIS 的计算机。 可以手动配置计算机，也可以使用配置 Web 同步向导。 建议您使用该向导。  
  
    > [!NOTE]  
    >  如果运行 IIS 的计算机运行的是 64 位版本的 Windows，则必须运行以下命令以确保该服务器为运行 Internet Server API (ISAPI) 应用程序进行了正确的配置。 有关详细信息，请参阅 IIS 文档。  
  
    ```  
    cscript %SystemDrive%\inetpub\AdminScripts\adsutil.vbs set w3svc/AppPools/Enable32bitAppOnWin64 1  
    ```  
  
4.  为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制侦听器设置相应权限。  
  
5.  在诊断模式下运行 Web 同步，以便测试与正在运行 IIS 的计算机的连接，并确保已正确安装 SSL 证书。  
  
## <a name="configuring-secure-sockets-layer"></a>配置安全套接字层  
 若要配置 SSL，请指定一个供正在运行 IIS 的计算机使用的证书。 用于合并复制的 Web 同步支持使用服务器证书，但不支持使用客户端证书。 若要为部署配置 IIS，就必须首先从证书颁发机构 (CA) 获取证书。 证书颁发机构是一个实体，负责确保属于用户、计算机或其他证书颁发机构的公共加密密钥的真实性并为其担保。 有关证书的详细信息，请参阅 IIS 文档。 安装证书后，必须使该证书与 Web 同步所用的网站相关联。  
  
#### <a name="to-specify-a-certificate-for-deployment"></a>为部署指定证书  
  
1.  以管理员身份登录到正在运行 IIS 的计算机。  
  
2.  启动 **“Internet Information Services(IIS)管理器”**：  
  
    1.  单击 **“开始”**，然后单击 **“运行”**。  
  
    2.  在 "**打开**" 框中`inetmgr`键入，然后单击 **"确定"**。  
  
3.  运行 IIS 证书向导：  
  
    1.  在 **“Internet 信息服务(IIS)管理器”** 中，展开 **“本地计算机”** 节点，然后展开 **“Web 站点”** 文件夹。  
  
    2.  右键单击 **“默认的 Web 站点”**，然后单击 **“属性”**。  
  
    3.  在 **“默认的 Web 站点属性”** 对话框中的 **“目录安全性”** 选项卡上，单击 **“服务器证书”**。  
  
    4.  完成 Web 服务器证书向导。  
  
4.  单击“确定”****。  
  
 如果无法从 CA 获得服务器证书，则可指定进行测试所需的证书。 若要为测试配置 IIS 6.0，请使用 SelfSSL 实用工具安装证书。 可从 IIS 6.0 资源工具包中获得该实用工具。 您可以从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=5135)下载这些工具。 对于 IIS 5.0，请转到 [Microsoft 帮助和支持](https://go.microsoft.com/fwlink/?LinkId=46229)。  
  
> [!NOTE]  
>  证书必须与网站相关联，该网站才能使用 SSL。 SelfSSL 自动使证书与默认网站相关联。 如果已有证书或以后从 CA 安装证书，则必须明确地使该证书与 Web 同步所使用的网站相关联。 确保只有一个与用于同步订阅的网站相关联的证书。 如果存在多个证书，订阅服务器将使用第一个可用网站。  
  
#### <a name="to-specify-a-certificate-for-testing-in-iis-60"></a>指定在 IIS 6.0 中进行测试所需的证书  
  
1.  以管理员身份登录到正在运行 IIS 的计算机。  
  
2.  下载并安装 SelfSSL。 默认情况下，应用程序将安装到 \<*驱动器*>:\Program Files\IIS Resources\SelfSSL。 应用程序和文档快捷方式将复制到 \<*驱动器*>:\Documents and Settings\All Users\Start Menu\Programs\IIS Resources\SelfSSL。  
  
3.  运行 SelfSSL：  
  
    -   若要用各参数的默认值运行 SelfSSL，请找到应用程序的安装目录，然后双击 SelfSSL.exe。  
  
        > [!NOTE]  
        >  默认情况下，SelfSSL 安装的证书有效期为七天。  
  
    -   若要指定一个或多个参数的值，请单击 **“开始”**，然后单击 **“运行”**。 在 "**打开**" 框中`cmd`，输入，然后单击 **"确定"**。 找到 SelfSSL 安装目录，键入 `SelfSSL`，然后指定一个或多个参数的值。 若要获得参数列表，请键入 `SelfSSL -?`。  
  
## <a name="installing-connectivity-components-and-sql-server-management-studio"></a>安装连接组件和 SQL Server Management Studio  
  
#### <a name="to-install-sql-server-connectivity-components-and-sql-server-management-studio"></a>安装 SQL Server 连接组件和 SQL Server Management Studio  
  
1.  以管理员身份登录到正在运行 IIS 的计算机。  
  
2.  从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 安装磁盘中启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装向导。 有关使用此向导的详细信息，请参阅安装[向导中的安装 SQL Server 2014 &#40;安装&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)。  
  
3.  在 **“功能选择”** 页中，选择 **“客户端工具连接”**。  
  
4.  如果计划使用配置 Web 同步向导，请选择 **“管理工具 – 基本”**。  
  
5.  完成该向导，然后重新启动计算机。  
  
    > [!NOTE]  
    >  可以安装其他组件，但 Web 同步仅需要连接组件。  
  
## <a name="configuring-the-computer-that-is-running-iis-by-using-the-configure-web-synchronization-wizard"></a>使用配置 Web 同步向导配置正在运行 IIS 的计算机  
 使用配置 Web 同步向导或以手动方式配置 IIS 服务器。 我们建议您使用向导，但同时在下一部分中提供手动配置的步骤。 
  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 随附的 Web 同步向导仅适用于在运行 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]的发布服务器上或在已经升级到 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]的发布服务器上创建的发布。 而不适用于 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]上的发布。 该向导适用于 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 及更高版本和 [!INCLUDE[ssEWnoversion](../../includes/ssewnoversion-md.md)] 3.0 及更高版本上的订阅。  
  
 该配置有以下特征：  
  
-   使用 IIS 中的默认网站。 但也可以使用其他网站。 有关如何创建网站的详细信息，请参阅 IIS 文档。  
  
    > [!NOTE]  
    >  通过指定的网站可访问 Web 同步使用的组件。 它不会提供对其他数据或网页的访问，除非将其如此配置。  
  
-   创建虚拟目录及其关联的别名。 访问 Web 同步组件时使用该别名。 例如，如果 IIS 地址是 https://*server.domain.com* ，而您指定了别名“websync1”，那么访问 replisapi.dll 组件的地址就是 https://*server.domain.com*/websync1/replisapi.dll。  
  
-   使用基本身份验证。 建议使用基本身份验证，因为它不需要 Kerberos 委托就可以在单独的计算机上运行 IIS 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布服务器/分发服务器（建议配置）。 将 SSL 与基本身份验证一起使用可以确保登录名、密码和所有数据都在传输中加密。 （无论使用何种身份验证类型，都需要 SSL。）有关 Web 同步的最佳实践的详细信息，请参阅[配置 Web 同步](configure-web-synchronization.md)中的 "Web 同步的最佳安全方案" 一节。  
  
#### <a name="to-configure-the-computer-that-is-running-iis-by-using-the-configure-web-synchronization-wizard"></a>使用配置 Web 同步向导配置正在运行 IIS 的计算机  
  
1.  在正在运行 IIS 的计算机上，启动 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
2.  连接至发布服务器，然后展开服务器节点。  
  
3.  展开 **“本地发布”** 文件夹，右键单击发布，然后单击 **“配置 Web 同步”**。  
  
4.  在配置 Web 同步向导中的 **“订阅服务器类型”** 页中，选择 **SQL Server**。  
  
5.  在 **“Web 服务器”** 页中：  
  
    1.  选择将同步订阅的 IIS 实例。  
  
    2.  选择 **“创建新的虚拟目录”**。  
  
    3.  在该页的底部窗格中，展开 IIS 实例，展开 **“网站”**，然后单击 **“默认网站”**。  
  
6.  在 **“虚拟目录信息”** 页中：  
  
    1.  在 **“别名”** 框中输入虚拟目录别名。  
  
    2.  在 **“路径”** 框中输入虚拟目录的路径。 例如，如果在 "**别名**" 框中输入`C:\Inetpub\wwwroot\websync1` `websync1` ，则在 "**路径**" 框中输入。 单击 **“下一步”**。  
  
    3.  在两个对话框中，单击 **“是”**。 这指定您要创建一个新文件夹并复制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Internet Server API (ISAPI) DLL。 .  
  
7.  在 **“经过身份验证的访问”** 页中：  
  
    1.  确保已清除 **“集成 Windows 身份验证”** 和 **“Windows 域服务器的摘要式身份验证”** 。  
  
    2.  选择 **“基本身份验证”**。  
  
    3.  在 **“默认域”** 和 **“领域”** 框中，输入正在运行 IIS 的计算机的域。  
  
8.  在 **“目录访问”** 页中：  
  
    1.  单击 **“添加”**，然后在 **“选择用户或组”** 对话框中添加订阅服务器在与 IIS 建立连接时将要使用的帐户。 你将在新建订阅向导的“Web 服务器信息”页中指定这些帐户或作为 **sp_addmergepullsubscription_agent**[](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql)* 参数的值指定它们。@internet_login*  
  
9. 在 **“快照共享访问”** 页中，输入快照共享。 在这个共享上设置相应权限，以使订阅服务器能够访问快照文件。 有关此共享的权限的详细信息，请参阅[保护快照文件](security/secure-the-snapshot-folder.md)。  
  
10. 在 **“完成向导”** 页中，单击 **“完成”**。  
  
     如果出现故障，例如尝试配置正在运行 IIS 的远程计算机时出现网络错误，就会回滚所有完成的操作并取消所有剩余操作。 如果无法回滚某项已完成的操作，则向导末页中的状态会显示 **“成功”** ，而已完成的操作会保持提交状态。  
  
11. 如果运行 IIS 的计算机是在 64 位版本的 Windows 上运行，则必须将 replisapi.dll 复制到相应目录：  
  
    1.  单击 **“开始”**，然后单击 **“运行”**。 在 "**打开**" 框中`iisreset`，输入，然后单击 **"确定"**。  
  
    2.  IIS 停止并重新启动后，将 replisapi.dll 从 [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]COM\replisapi 复制到步骤 6b 中指定的目录。  
  
    3.  单击 **“开始”**，然后单击 **“运行”**。 在 "**打开**" 框中`cmd`，输入，然后单击 **"确定"**。  
  
    4.  在步骤 6b 指定的目录中，执行以下命令：  
  
         `regsvr32 replisapi.dll`  
  
## <a name="manually-configuring-the-computer-that-is-running-iis"></a>手动配置正在运行 IIS 的计算机  
 若要手动配置正在运行 IIS 的计算机，必须安装和配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制侦听器，然后为将连接到 IIS 的订阅服务器配置授权。  
  
#### <a name="to-install-and-configure-the-sql-server-replication-listener"></a>安装和配置 SQL Server 复制侦听器  
  
1.  在正在运行 IIS 的计算机上创建一个文件目录，用来存放 replisapi.dll。 可在任意所需位置创建该目录，但建议将该目录创建在 \<*驱动器*>:\Inetpub 目录下。 例如，可以创建目录 \<*驱动器*>:\Inetpub\SQLReplication\\。  
  
    > [!IMPORTANT]  
    >  极力建议在 NTFS 文件系统分区中（而不是 FAT 文件系统中）创建此目录。 使用 NTFS 文件系统时，可以用 NTFS 文件系统权限来精确控制可以访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制的用户。  
  
2.  将 replisapi.dll 从目录 [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]com\ 复制到在步骤 1 中创建的文件目录。  
  
3.  注册 replisapi.dll：  
  
    1.  单击 **“开始”**，然后单击 **“运行”**。 在 "**打开**" 框中`cmd`，输入，然后单击 **"确定"**。  
  
    2.  在步骤 1 创建的目录中，执行以下命令：  
  
         `regsvr32 replisapi.dll`  
  
4.  创建一个用于复制的新网站，或使用现有网站。 复制组件将在同步过程中访问该网站。 有关如何创建网站的详细信息，请参阅 IIS 文档。  
  
5.  在 IIS 上创建一个虚拟目录。 虚拟目录应在步骤 4 所创建的网站下创建，并将其映射到步骤 1 中创建的目录。 有关如何创建虚拟目录的详细信息，请参阅 IIS 文档。 建议尽量限制为该目录分配权限。 必须选择 **“读取”** 和 **“执行”** 权限，但可以清除 **“运行脚本”**、 **“写入”** 和 **“浏览”** 权限。  
  
6.  配置 IIS 以允许执行 replisapi.dll。 步骤 4 中分配的权限对 IIS 的早期版本足够了，但 IIS 6.0 版要求启用 Internet Server API (ISAPI) 扩展。 有关详细信息，请参阅 IIS 6.0 文档中的“配置 ISAPI 扩展”和“启用和禁用动态目录”。  
  
#### <a name="to-configure-iis-authentication"></a>配置 IIS 身份验证  
  
-   当订阅方连接到 IIS 时，IIS 必须对其进行身份验证，订阅方才能访问资源和过程。 IIS 提供了三种类型的身份验证：匿名、基本和集成。 身份验证可以应用于整个网站或您创建的虚拟目录。  
  
     建议您使用带有 SSL 的基本身份验证。 无论使用何种类型的身份验证，都需要 SSL。 有关如何配置身份验证的详细信息，请参阅 IIS 文档。  
  
## <a name="setting-permissions-for-the-sql-server-replication-listener"></a>设置 SQL Server 复制侦听器的权限  
 订阅服务器连接到正在运行 IIS 的计算机时，将使用您在配置 IIS 时指定的身份验证类型对订阅服务器进行身份验证。 IIS 对订阅服务器进行身份验证后，IIS 将检查订阅服务器是否有权调用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制。 通过设置 replisapi.dll 权限可以控制能够调用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制的用户。 适当的权限配置对于防止在未经授权的情况下访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制而言很有必要。  
  
 若要配置运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制侦听器的帐户的最低权限，请完成以下过程。 此过程中的步骤适用[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]于运行 IIS 6.0。  
  
 除了要执行下列步骤之外，请确保所需的登录名存在于发布访问列表 (PAL) 中。 有关 PAL 的详细信息，请参阅[保护发布服务器](security/secure-the-publisher.md)。  
  
#### <a name="to-configure-the-account-and-permissions"></a>配置帐户和权限  
  
1.  在运行 IIS 的计算机上创建一个本地帐户：  
  
    1.  右键单击“我的电脑”****，然后单击“管理”****。  
  
    2.  在 **“计算机管理”** 中，展开 **“本地用户和组”**。  
  
    3.  右键单击 **“用户”**，然后单击 **“新建用户”**。  
  
    4.  输入用户名和强密码。  
  
    5.  单击 **“创建”**，然后单击 **“关闭”**。  
  
2.  将帐户添加到 IIS_WPG 组：  
  
    1.  在 **“计算机管理”** 中，展开 **“本地用户和组”**，然后单击 **“组”**。  
  
    2.  右键单击 **IIS_WPG**，然后单击 **“添加到组”**。  
  
    3.  在 **“IIS_WPG 属性”** 对话框中，单击 **“添加”**。  
  
    4.  在 **“选择用户、计算机或组”** 对话框中，添加在步骤 1 中创建的帐户。  
  
    5.  确保 **“从此位置”** 字段中为本地计算机（而不是域）的名称。 如果不是本地计算机的名称，请单击 **“位置”**。 在 **“位置”** 对话框中，选择本地计算机，然后单击 **“确定”**。  
  
    6.  在 **“选择用户”** 对话框和 **“IIS_WPG 属性”** 对话框中，单击 **“确定”**。  
  
3.  将包含 replisapi.dll 的文件夹的最低权限授予帐户：  
  
    1.  找到为 replisapi.dll 创建的文件夹，右键单击该文件夹，再单击 **“共享和安全”**。  
  
    2.  在“安全”**** 选项卡上，单击“添加”****。  
  
    3.  在 **“选择用户、计算机或组”** 对话框中，添加在步骤 1 中创建的帐户。  
  
    4.  确保 **“从此位置”** 字段中为本地计算机（而不是域）的名称。 如果不是本地计算机的名称，请单击 **“位置”**。 在 **“位置”** 对话框中，选择本地计算机，然后单击 **“确定”**。  
  
    5.  请确保只向该帐户授予“读取”、“读取和执行”和“列出文件夹内容”权限。************  
  
    6.  选择所有不需要访问该目录的用户或组，然后单击 **“删除”**。  
  
    7.  单击“确定”****。  
  
4.  在 **“Internet 信息服务(IIS)管理器”** 中创建应用程序池：  
  
    1.  单击 **“开始”**，然后单击 **“运行”**。  
  
    2.  在 "**打开**" 框中`inetmgr`键入，然后单击 **"确定"**。  
  
    3.  在 **“Internet 信息服务(IIS)管理器”** 中，展开 **“本地计算机”** 节点。  
  
    4.  右键单击 **“应用程序池”**，指向 **“新建”** ，然后单击 **“应用程序池”**。  
  
    5.  在 **“应用程序池 ID”** 字段中，输入池的名称，然后单击 **“确定”**。  
  
5.  将帐户与应用程序池关联：  
  
    1.  在 **“Internet 信息服务(IIS)管理器”** 中，展开 **“本地计算机”** 节点，然后展开 **“应用程序池”**。  
  
    2.  右键单击所创建的应用程序池，然后单击 **“属性”**。  
  
    3.  在** \<ApplicationPoolName> 属性**"对话框的"**标识**"选项卡上，单击"**可配置**"。  
  
    4.  在 **“用户名”** 和 **“密码”** 字段中，输入在步骤 1 中创建的帐户和密码。  
  
    5.  单击“确定”****。  
  
6.  将应用程序池与用于 Web 同步的虚拟目录关联：  
  
    1.  在 **“Internet 信息服务(IIS)管理器”** 中，展开 **“本地计算机”** 节点，再展开 **“网站”**。  
  
    2.  展开当前用于 Web 同步的网站，右键单击为 Web 同步所创建的虚拟目录，然后单击 **“属性”**。  
  
    3.  在“**VirtualDirectoryName> 属性”对话框的“虚拟目录”选项卡上，从“应用程序池”下拉列表中选择在步骤 5 中创建的应用程序池。****\<******  
  
    4.  单击“确定”****。  
  
## <a name="testing-the-connection-to-replisapidll"></a>测试到 replisapi.dll 的连接  
 在诊断模式下运行 Web 同步，以便测试与正在运行 IIS 的计算机的连接，并确保已正确安装安全套接字层 (SSL) 证书。 若要在诊断模式下运行 Web 同步，您必须是运行 IIS 的计算机中的管理员。  
  
#### <a name="to-test-the-connection-to-replisapidll"></a>测试到 replisapi.dll 的连接  
  
1.  确保订阅服务器中的局域网 (LAN) 设置正确：  
  
    1.  在[!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer 的 "**工具**" 菜单上，单击 " **Internet 选项**"。  
  
    2.  在 **“连接”** 选项卡上，单击 **“局域网设置”**。  
  
    3.  如果 LAN 中未使用代理服务器，请清除 **“自动检测设置”** 和 **“为 LAN 使用代理服务器”**。  
  
    4.  如果使用了代理服务器，请选择 **“为 LAN 使用代理服务器”** 和 **“对于本地地址不使用代理服务器”**。  
  
    5.  单击“确定”****。  
  
2.  在订阅服务器上的 Internet Explorer 中，用向 replisapi.dll 的地址追加 `?diag` 的方法以诊断模式连接到服务器。 例如：https://server.domain.com/directory/replisapi.dll?diag。  
  
3.  如果 Windows 操作系统不能识别您为 IIS 指定的证书，则会显示 **“安全警报”** 对话框。 如果该证书是测试证书或是由 Windows 不能识别的证书颁发机构 (CA) 颁发的证书，便会显示该警报。  
  
    > [!NOTE]  
    >  如果未出现此对话框，请确保您所访问的服务器的证书已作为可信证书添加到订阅服务器的证书存储区。 有关导出证书的详细信息，请参阅 IIS 文档。  
  
    1.  在 **“安全警报”** 对话框中，单击 **“查看证书”**。  
  
    2.  在 **“证书”** 对话框的 **“常规”** 选项卡上，单击 **“安装证书”**。  
  
    3.  完成证书导入向导，接受默认值。  
  
    4.  在 **“安全警告”** 对话框中，单击 **“是”**。  
  
    5.  在“证书导入向导”确认对话框中，单击 **“确定”**。  
  
    6.  关闭 **“证书”** 对话框。  
  
    7.  在 **“安全警报”** 对话框中，单击 **“是”**。  
  
    > [!NOTE]  
    >  为用户安装证书。 必须为要与 IIS 同步的每个用户执行该过程。  
  
4.  在“连接到 **服务器名>”对话框框中，指定合并代理将用于连接到 IIS 的登录名和密码。\<** 在新建订阅向导中也要指定这些凭据。  
  
5.  在名为 **“SQL Websync 诊断信息”** 的 Internet Explorer 窗口中，验证该页中每个 **“状态”** 列的值是否都为 **SUCCESS**。  
  
6.  确保证书已正确安装到订阅服务器中：  
  
    1.  关闭并重新打开 Internet Explorer。  
  
    2.  以诊断模式连接到服务器。 如果证书安装正确，就不会显示 **“安全警报”** 对话框。 如果显示了该对话框，那么合并代理试图连接到正在运行 IIS 的计算机时就会失败。 必须确保您所访问的服务器的证书已作为可信证书添加到订阅服务器的证书存储区。 有关导出证书的详细信息，请参阅 IIS 文档。  
  
## <a name="see-also"></a>另请参阅  
 [配置 Web 同步](configure-web-synchronization.md)  
  
  
