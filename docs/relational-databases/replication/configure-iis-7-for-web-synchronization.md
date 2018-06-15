---
title: 配置 IIS 7 以实现 Web 同步 | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- IIS 7 server configuration [SQL Server replication]
- Web synchronization, IIS 7 servers
ms.assetid: c201fe2c-0a76-44e5-a233-05e14cd224a6
caps.latest.revision: 11
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ebf8cefa129638c36fa37b081ffcb345a2c49f54
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32957482"
---
# <a name="configure-iis-7-for-web-synchronization"></a>配置 IIS 7 以实现 Web 同步
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  本主题介绍手动配置 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS) 版本 7 及更高版本的完整过程，以便与用于合并复制的 Web 同步一起使用。 
  
 配置 IIS 7 或更高版本是启用 Web 同步所需的三个步骤中的第一步。  
  
 有关整个配置过程的概述，请参阅[配置 Web 同步](../../relational-databases/replication/configure-web-synchronization.md)。  
  
> [!IMPORTANT]  
>  请确保您的应用程序仅使用 [!INCLUDE[dnprdnlong](../../includes/dnprdnlong-md.md)] 或更高版本，并且 IIS 服务器上没有安装 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 的较早版本。 较早版本的 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 可能引起错误，如：“Web 同步期间出现的消息的格式无效。 请确保在 Web 服务器上正确配置了复制组件。”。  
  
 若要使用 Web 同步，必须通过完成以下步骤来配置 IIS。 本主题对每个步骤都进行了详细说明。  
  
1.  在运行 IIS 的计算机上安装和配置 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制侦听器。  
  
2.  配置安全套接字层 (SSL)。 IIS 和所有订阅服务器之间的通信需要 SSL。  
  
3.  配置 IIS 身份验证。  
  
4.  为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制侦听器配置帐户并设置权限。  
  
## <a name="installing-the-sql-server-replication-listener"></a>安装 SQL Server 复制侦听器  

从版本 5.0 开始，IIS 中支持 Web 同步。 IIS 版本 5 和 6 的“配置 Web 同步向导”不可与 IIS 版本 7.0 和更高版本一起使用。 **从 SQL Server 2012 开始，要使用 IIS 服务器上的 Web 同步组件，应当随复制安装 SQL Server。这可以是免费的 SQL Server Express 版本。**
  
#### <a name="to-install-and-configure-the-sql-server-replication-listener"></a>安装和配置 SQL Server 复制侦听器  
  
1.  在 IIS 计算机上安装 SQL Server 复制。

2. 在正在运行 IIS 的计算机上为 replisapi.dll 创建一个新的文件目录。 可在任意所需位置创建该目录，但建议将该目录创建在 \<*驱动器*>:\Inetpub 目录下。 例如，可以创建目录 \<*驱动器*>:\Inetpub\SQLReplication\\。  
  
3.  将 replisapi.dll 从目录 [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]com\ 复制到在步骤 1 中创建的文件目录。  
  
4.  注册 replisapi.dll：  
  
    1.  单击 **“启动”**，再单击 **“运行”**。 在“打开”  框中，输入 **cmd**，然后单击“确定” 。  
  
    2.  在步骤 1 所创建的目录中，执行以下命令：  
  
         **regsvr32 replisapi.dll**  
  
5.  创建一个用于复制的新网站或使用现有网站。 复制组件将在同步过程中访问此网站。 本主题中的过程将假定使用“默认网站”。 有关如何创建网站的详细信息，请参阅 IIS 文档。  
  
6.  在 IIS 上创建一个虚拟目录。 应在步骤 4 所创建的网站下创建虚拟目录，并将其映射到步骤 1 中创建的目录。 建议尽量限制为此目录分配权限。 您必须至少选择 **“读取”** 权限和 **“执行”** 权限。  
  
    1.  在 **“Internet 信息服务(IIS)管理器”** 的 **“连接”** 窗格中，右键单击 **“默认网站”**，然后选择 **“添加虚拟目录”**。  
  
    2.  对于“别名” ，请输入 **SQLReplication**。  
  
    3.  对于“物理路径”，输入 **\<驱动器>:\Inetpub\SQLReplication\\**，然后单击“确定”。  
  
7.  配置 IIS 以允许执行 replisapi.dll。  
  
    1.  在 **“Internet 信息服务(IIS)管理器”** 中，单击 **“默认网站”**。  
  
    2.  在中央窗格中，单击 **“处理程序映射”**。  
  
    3.  在 **“操作”** 窗格中，单击 **“添加模块映射”**。  
  
    4.  对于“请求”  路径，请输入 **replisapi.dll**。  
  
    5.  从 **“模块”** 下拉列表中，选择 **“IsapiModule”**。  
  
    6.  对于“可执行文件”，输入 **\<驱动器>:\Inetpub\SQLReplication\replisapi.dll**。  
  
    7.  对于“名称” ，请输入 **Replisapi**。  
  
    8.  依次单击 **“请求限制”** 按钮、 **“访问”** 选项卡和 **“执行”**。  
  
    9. 单击 **“确定”** 关闭 **“请求限制”** 对话框，然后再次单击 **“确定”** 关闭 **“添加模块映射”** 对话框。 在系统提示您允许使用 ISAPI 扩展插件后，单击 **“是”** 以添加该扩展插件。  
  
    10. 检查 Replisapi.dll 是否列在 **“已启用”** 处理程序映射下。 如果它列在 **“已禁用”** 列表中，请右键单击 Replisapi 条目，然后单击 **“编辑功能权限”**。 选中 **“执行”** 框，然后单击 **“确定”**。  
  
## <a name="configuring-iis-authentication"></a>配置 IIS 身份验证  
 当订阅服务器计算机连接到 IIS 时，订阅服务器必须经过 IIS 的身份验证才能访问资源和过程。 身份验证可以应用于整个网站或您创建的虚拟目录。  
  
 建议您使用带有 SSL 的基本身份验证。 无论使用何种类型的身份验证，都需要 SSL。  
  
 建议您使用带有 SSL 的基本身份验证。 无论使用何种类型的身份验证，都需要 SSL。  
  
#### <a name="to-configure-iis-authentication"></a>配置 IIS 身份验证  
  
1.  在 **“Internet 信息服务(IIS)管理器”** 中，单击 **“默认网站”**。  
  
2.  在中间窗格中，双击 **“身份验证”**。  
  
3.  右键单击“匿名身份验证”，然后选择“禁用”。  
  
4.  右键单击“基本身份验证”，然后选择“启用”。  
  
## <a name="configuring-secure-sockets-layer"></a>配置安全套接字层  
 若要配置 SSL，请指定一个供正在运行 IIS 的计算机使用的证书。 用于合并复制的 Web 同步支持使用服务器证书，但不支持使用客户端证书。 若要为部署配置 IIS，就必须首先从证书颁发机构 (CA) 获取证书。 有关证书的详细信息，请参阅 IIS 文档。  
  
 安装证书后，必须使该证书与 Web 同步所用的网站相关联。 出于开发和测试目的，可以指定自签名证书。 IIS 7 可以为您创建证书并在计算机上注册该证书。  
  
 为生产环境进行部署与在此给出的过程之间的差异在于：在生产和产前测试环境中，您需要使用由 CA 颁发的证书而不是自签名证书。  
  
> [!IMPORTANT]  
>  不建议对生产环境中的安装使用自签名证书， 因为自签名证书不安全。 仅将自签名证书用于开发和测试目的。  
  
 若要配置 SSL，您需要执行以下步骤：  
  
1.  配置网站要求 SSL 并忽略客户端证书。  
  
2.  从 CA 获得证书或创建自签名证书。  
  
3.  将证书绑定到复制网站。  
  
#### <a name="to-require-ssl-security-for-a-web-site"></a>要求对网站设置 SSL 安全性  
  
1.  在 **“Internet 信息服务(IIS)管理器”** 中，展开本地服务器节点，然后单击 **“默认网站”** （或是不同于默认网站的 Web 同步站点）。  
  
2.  在中间窗格中，双击 **“SSL 设置”**。  
  
3.  选中 **“要求 SSL”** 选项。 在 **“客户端证书”** 下，确保已选中 **“忽略”** 按钮。  
  
#### <a name="to-create-a-self-signed-certificate-for-testing"></a>创建用于测试的自签名证书  
  
1.  在 **“Internet 信息服务(IIS)管理器”** 中，单击本地服务器节点，然后在中央窗格中双击 **“服务器证书”**。  
  
2.  在 **“操作”** 窗格中，单击 **“创建自签名证书”**。  
  
3.  在 **“创建自签名证书”** 对话框中，输入证书名称，然后单击 **“确定”**。  
  
###### <a name="to-bind-a-certificate-to-a-web-site"></a>将证书绑定到网站  
  
1.  在 **“连接”** 窗格中，单击 **“默认网站”** （或是不同于默认网站的 Web 同步站点）。  
  
2.  在 **“操作”** 窗格中，依次单击 **“绑定”** 和 **“添加”**。 **“添加网站绑定”** 对话框将出现。  
  
3.  从 **“类型”** 下拉列表中，选择 **“https”**。 保留 **“IP 地址”** 和 **“端口”** 的默认设置。  
  
4.  从 **“SSL 证书”** 下拉列表中，选择在“创建用于测试的自签名证书”中创建的证书，单击 **“确定”**，然后单击 **“关闭”**。  
  
###### <a name="to-test-the-certificate"></a>测试证书  
  
1.  在 **在ternet 在formation Services (IIS) Manager**中，单击 **“默认网站”.**  
  
2.  从“操作”窗格中，单击“浏览 \*:443(https)”。  
  
3.  Internet Explorer 随即打开并显示一条消息“此网站的安全证书有问题。”。 此警告向您表明关联的证书不是由认可的 CA 颁发的，因此可能不值得信任。 这个警告在意料之中，只需单击 **“继续浏览此网站(不推荐)”**。  
  
4.  如果系统提示您 **“连接至 localhost”**，请输入用户名和密码继续操作。 此时应能看到该网站的默认页面。  
  
## <a name="setting-permissions-for-the-sql-server-replication-listener"></a>设置 SQL Server 复制侦听器的权限  
 订阅服务器计算机连接到正在运行 IIS 的计算机时，将使用您在配置 IIS 时指定的身份验证类型对该订阅服务器进行身份验证。 IIS 对订阅服务器进行身份验证后，IIS 将检查该订阅服务器是否有权调用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制。 通过设置 replisapi.dll 权限可以控制能够调用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制的用户。 适当的权限配置对于防止在未经授权的情况下访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制而言很有必要。  
  
 若要配置运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制侦听器的帐户的最低权限，请完成以下过程。 以下过程中的步骤适用于运行 IIS 7.0 的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Server 2008。  
  
 除了要执行下列步骤之外，请确保所需的登录名存在于发布访问列表 (PAL) 中。 有关 PAL 的详细信息，请参阅[保护发布服务器](../../relational-databases/replication/security/secure-the-publisher.md)。  
  
 **重要提示** 本节中创建的帐户就是要在同步期间连接到发布服务器和分发服务器的帐户。 此帐户必须作为 SQL 登录帐户添加到分发服务器和发布服务器上。  
  
 用于 SQL Server 复制侦听器的帐户必须具有“合并代理安全性”主题中的“连接发布服务器或分发服务器”一节所述的权限。  
  
 总之，该帐户必须：  
  
-   是发布访问列表 (PAL) 的成员。  
  
-   映射到与发布数据库中的某个用户关联的登录名。  
  
-   映射到与分发数据库中的某个用户关联的登录名。  
  
-   对快照共享具有读取权限。  
  
#### <a name="to-configure-the-account-and-permissions"></a>配置帐户和权限  
  
1.  在运行 IIS 的计算机上创建一个本地帐户：  
  
    1.  打开 **“服务器管理器”**。 从“开始”菜单，右键单击 **“计算机”**，然后单击 **“管理”**。  
  
    2.  在 **“服务器管理器”** 中，展开 **“配置”**，然后展开 **“本地用户和组”**。  
  
    3.  右键单击 **“用户”**，然后单击 **“新建用户”**。  
  
    4.  输入用户名和强密码。 清除 **“用户在下次登录时必须更改密码”**。  
  
    5.  单击 **“创建”**，然后单击 **“关闭”**。  
  
2.  将帐户添加到 IIS_IUSRS 组：  
  
    1.  在 **“服务器管理器”** 中，依次展开 **“配置”** 和 **“本地用户和组”**，然后单击 **“组”**。  
  
    2.  右键单击 **“IIS_IUSRS”**，然后单击 **“添加到组”**。  
  
    3.  在 **“IIS_IUSRS 属性”** 对话框中，单击 **“添加”**。  
  
    4.  在 **“选择用户、计算机或组”** 对话框中，添加在步骤 1 中创建的帐户。  
  
    5.  确保 **“从此位置”** 显示的是本地计算机（而不是域）的名称。 如果此字段不显示本地计算机名称，请单击 **“位置”**。 在 **“位置”** 对话框中，选择本地计算机，然后单击 **“确定”**。  
  
    6.  在“选择用户”  对话框和“IIS_IUSRS 属性”  对话框中，单击“确定”。  
  
3.  对包含 replisapi.dll 的文件夹授予最低帐户权限：  
  
    1.  在 Windows Explorer 中，右键单击为 replisapi.dll 创建的文件夹，然后单击 **“属性”**。  
  
    2.  在 **“安全性”** 选项卡上，单击 **“编辑”**。  
  
    3.  在“\<文件夹名> 的权限”对话框中，单击“添加”以添加在步骤 1 中创建的帐户。  
  
    4.  确保 **“从此位置”** 显示的是本地计算机（而不是域）的名称。 如果此字段不显示本地计算机名称，请单击 **“位置”**。 在 **“位置”** 对话框中，选择本地计算机，然后单击 **“确定”**。  
  
    5.  验证是否仅向该帐户授予了“读取”、“读取和执行”和“列出文件夹内容”权限。  
  
    6.  选择所有不需要访问该目录的用户或组，然后依次单击 **“删除”** 和 **“确定”**。  
  
4.  在 **“Internet 信息服务(IIS)管理器”** 中创建应用程序池：  
  
    1.  在 **“Internet 信息服务(IIS)管理器”** 中的 **“连接”** 窗格中，展开本地服务器节点。  
  
    2.  右键单击 **“应用程序池”**，然后单击 **“添加应用程序池”**。  
  
    3.  输入应用程序池的名称，保留其余字段中的默认值，然后单击 **“确定”**。  
  
    > [!NOTE]  
    >  如果您预计并发同步客户端超过两个，则最好创建 Web 园。 有关详细信息，请参阅[配置 Web 同步](../../relational-databases/replication/configure-web-synchronization.md)中的“创建 Web 园”。  
  
5.  将帐户与应用程序池关联：  
  
    1.  在 **“Internet 信息服务(IIS)管理器”** 中，展开本地服务器节点，然后单击 **“应用程序池”**。  
  
    2.  右键单击所创建的应用程序池，然后单击 **“设置应用程序池默认设置”**。  
  
    3.  在 **“应用程序池默认设置”** 对话框中，向下滚动到 **“处理模型”** 部分，然后单击 **“标识”** 字段。  
  
    4.  单击 **“标识”** 行右侧的省略号按钮。  
  
    5.  单击 **“自定义帐户”** 单选按钮，然后单击 **“设置”**。  
  
    6.  在 **“用户名”** 和 **“密码”** 字段中，输入在步骤 1 中创建的帐户和密码，然后单击 **“确定”**。  
  
    7.  单击“确定”  关闭“应用程序池标识”  对话框，然后再次单击  “确定”关闭 “应用程序池默认设置”对话框。  
  
6.  将应用程序池与复制网站关联：  
  
    1.  在 **“Internet 信息服务(IIS)管理器”** 中，展开本地服务器节点，然后单击 **“默认网站”** （或是不同于默认网站的 Web 同步站点）。  
  
    2.  在 **“操作”** 窗格中的 **“管理网站”** 下，单击 **“高级设置”**。  
  
    3.  在 **“高级设置”** 对话框中，单击 **“应用程序池”** 右侧的省略号按钮。  
  
    4.  从 **“应用程序池”** 下拉列表中，选择您在步骤 4 中创建的应用程序池，然后单击 **“确定”**。  
  
    5.  再次单击 **“确定”** ，关闭“高级设置”。  
  
## <a name="testing-the-connection-to-replisapidll"></a>测试到 replisapi.dll 的连接  
 在诊断模式下运行 Web 同步，以便测试与正在运行 IIS 的计算机的连接，并确保已正确安装安全套接字层 (SSL) 证书。 若要在诊断模式下运行 Web 同步，您必须是运行 IIS 的计算机中的管理员。  
  
#### <a name="to-test-the-connection-to-replisapidll"></a>测试到 replisapi.dll 的连接  
  
1.  确保订阅服务器中的局域网 (LAN) 设置正确：  
  
    1.  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer 中的 **“工具”** 菜单中，单击 **“Internet 选项”**。  
  
    2.  在 **“连接”** 选项卡上，单击 **“局域网设置”**。  
  
    3.  如果 LAN 中未使用代理服务器，请清除 **“自动检测设置”** 和 **“为 LAN 使用代理服务器”**。  
  
    4.  如果使用了代理服务器，请单击 **“为 LAN 使用代理服务器”** 和 **“对于本地地址不使用代理服务器”**，然后单击 **“确定”**。  
  
2.  在订阅服务器上的 Internet Explorer 中，用向 replisapi.dll 的地址追加 `?diag` 的方法以诊断模式连接到服务器。 例如： `https://server.domain.com/directory/replisapi.dll?diag`。  
  
    > [!NOTE]  
    >  在上例中， **server.domain.com** 应原样替换为在 IIS 管理器的 **“服务器证书”** 部分中列出的 **“颁发给”** 名称。  
  
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
  
4.  在“连接到 \<服务器名>”对话框框中，指定合并代理将用于连接到 IIS 的登录名和密码。 在新建订阅向导中也要指定这些凭据。  
  
5.  在名为 **“SQL Websync 诊断信息”** 的 Internet Explorer 窗口中，验证该页中每个 **“状态”** 列的值是否都为 **SUCCESS**。  
  
6.  确保证书已正确安装到订阅服务器中：  
  
    1.  关闭并重新打开 Internet Explorer。  
  
    2.  以诊断模式连接到服务器。 如果证书安装正确，就不会显示 **“安全警报”** 对话框。 如果显示了该对话框，那么合并代理试图连接到正在运行 IIS 的计算机时就会失败。 必须确保您所访问的服务器的证书已作为可信证书添加到订阅服务器的证书存储区。 有关导出证书的详细信息，请参阅 IIS 文档。  
  
## <a name="see-also"></a>另请参阅  
 [合并复制的 Web 同步](../../relational-databases/replication/web-synchronization-for-merge-replication.md)   
 [配置 Web 同步](../../relational-databases/replication/configure-web-synchronization.md)  
  
  
