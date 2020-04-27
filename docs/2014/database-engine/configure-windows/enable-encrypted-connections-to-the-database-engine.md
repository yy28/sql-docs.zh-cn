---
title: 启用到数据库引擎（SQL Server 配置管理器）的加密连接 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], encrypted
- SSL [SQL Server]
- Secure Sockets Layer (SSL)
- encryption [SQL Server], connections
- cryptography [SQL Server], connections
- certificates [SQL Server], installing
- requesting encrypted connections
- installing certificates
- security [SQL Server], encryption
ms.assetid: e1e55519-97ec-4404-81ef-881da3b42006
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a872057f354b289d65a6a3a730e3a63afd7af0d4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62782311"
---
# <a name="enable-encrypted-connections-to-the-database-engine-sql-server-configuration-manager"></a>启用数据库引擎的加密连接（SQL Server 配置管理器）
  本主题介绍如何通过使用 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 配置管理器为 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 指定证书来启用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的加密连接。 服务器计算机必须具有提供的证书，客户端计算机必须设置为信任该证书的根颁发机构。 提供是指通过将证书导入 Windows 来安装证书的过程。  
  
 必须颁发证书才能进行 **服务器身份验证**。 证书名称必须为计算机的完全限定域名 (FQDN)。  
  
 用户的证书存储在本地计算机上。 若要安装证书以供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用，必须使用运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务时所用的用户帐户来运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器，除非该服务作为 LocalSystem、NetworkService 或 LocalService 运行（在这种情况下，可以使用管理帐户）。  
  
 客户端必须能够验证服务器所用证书的所有权。 如果客户端具有对服务器证书进行签名的证书颁发机构所颁发的公钥证书，则不需要进一步的配置。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 包含多个证书颁发机构所颁发的公钥证书。 如果服务器证书由公共或私人证书颁发机构进行签名，而客户端没有该机构颁发的公钥证书，则必须安装对服务器证书进行签名的证书颁发机构所颁发的公钥证书。  
  
> [!NOTE]  
>  若要在故障转移群集中使用加密，必须在故障转移群集的所有节点上安装带有虚拟服务器的完全限定 DNS 名称的服务器证书。 例如，如果你有一个具有名为 test1 的节点的双节点群集。公司>.com 和 test2。 * \< *你的公司>.com，你有一个名为 virtsql 的虚拟服务器，需要为 virtsql 安装一个证书。 * \< *你的公司在两个节点上都>.com。 * \< * 可以将“ForceEncryption”**** 选项的值设置为“是”****。  
  
 **本主题内容**  
  
-   **若要允许加密连接：**  
  
     [在服务器上设置（安装）证书](#Provision)  
  
     [导出服务器证书](#Export)  
  
     [将服务器配置为接受加密连接](#ConfigureServerConnections)  
  
     [将客户端配置为请求加密连接](#ConfigureClientConnections)  
  
     [通过 SQL Server Management Studio 加密连接](#EncryptConnection)  
  
##  <a name="SSMSProcedure"></a>  
  
###  <a name="to-provision-install-a-certificate-on-the-server"></a><a name="Provision"></a> 在服务器中提供（安装）证书  
  
1.  在 "**开始**" 菜单上，单击 "**运行**"，然后在 " `MMC` **打开**" 框中键入，然后单击 **"确定"**。  
  
2.  在 MMC 控制台中的“文件”**** 菜单上，单击“添加/删除管理单元”****。  
  
3.  在“添加/删除管理单元”**** 对话框中，单击“添加”****。  
  
4.  在“添加独立管理单元”**** 对话框中，单击“证书”****，再单击“添加”****。  
  
5.  在“证书管理单元”**** 对话框中，单击“计算机帐户”****，再单击“完成”****。  
  
6.  在“添加独立管理单元”**** 对话框中，单击“关闭”****。  
  
7.  在“添加/删除管理单元”**** 对话框中，单击“确定”****。  
  
8.  在“证书”**** 管理单元中，依次展开“证书”**** 和“个人”****，右键单击“证书”****，指向“所有任务”****，然后单击“导入”****。  
  
9. 完成 **证书导入向导**，将证书添加到计算机中，然后关闭 MMC 控制台。 有关向计算机添加证书的详细信息，请参阅 Windows 文档。  
  
###  <a name="to-export-the-server-certificate"></a><a name="Export"></a> 导出服务器证书  
  
1.  在“证书”**** 管理单元中的“证书”**** / “个人”**** 文件夹中找到证书，右键单击“证书”****，指向“所有任务”****，然后单击“导出”****。  
  
2.  完成 **“证书导出向导”**，将证书文件存储在方便的位置。  
  
###  <a name="to-configure-the-server-to-accept-encrypted-connections"></a><a name="ConfigureServerConnections"></a> 将服务器配置为接受加密连接  
  
1.  在“SQL Server 配置管理器”中，展开“SQL Server 网络配置”，右键单击“\<服务器实例> 协议”，然后选择“属性”************ __****。  
  
2.  在 " **Protocols for**_\<实例名称_的协议>**属性**" 对话框中的 "**证书**" 选项卡上，从 "**证书**" 框的下拉菜单中选择所需的证书，然后单击 **"确定"**。  
  
3.  在 **“标志”** 选项卡的 **“ForceEncryption”** 框中，选择 **“是”**，然后单击 **“确定”** 关闭该对话框。  
  
4.  重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务。  
  
###  <a name="to-configure-the-client-to-request-encrypted-connections"></a><a name="ConfigureClientConnections"></a> 将客户端配置为请求加密连接  
  
1.  将原始证书或导出的证书文件复制到客户端计算机。  
  
2.  在客户端计算机上，使用“证书”**** 管理单元来安装根证书或导出的证书文件。  
  
3.  在控制台窗格中，右键单击“SQL Server Native Client 配置”****，再单击“属性”****。  
  
4.  在 **“标志”** 选项卡的 **“强制协议加密”** 框中，单击 **“是”**。  
  
###  <a name="to-encrypt-a-connection-from-sql-server-management-studio"></a><a name="EncryptConnection"></a> 通过 SQL Server Management Studio 加密连接  
  
1.  在对象资源管理器工具栏上，单击 **“连接”**，再单击 **“数据库引擎”**。  
  
2.  在 **“连接到服务器”** 对话框中，填写连接信息，然后单击 **“选项”**。  
  
3.  在 **“连接属性”** 选项卡上，单击 **“加密连接”**。  
  
  
