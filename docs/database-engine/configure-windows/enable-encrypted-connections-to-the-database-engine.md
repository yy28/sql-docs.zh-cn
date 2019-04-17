---
title: 启用数据库引擎的加密连接 | Microsoft Docs
ms.custom: ''
ms.date: 04/09/2019
ms.prod: sql
ms.prod_service: security
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
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 28a2c9bd527fb4996730630a6121d205fbaebf04
ms.sourcegitcommit: 5f38c1806d7577f69d2c49e66f06055cc1b315f1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59429343"
---
# <a name="enable-encrypted-connections-to-the-database-engine"></a>启用数据库引擎的加密连接
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  本主题介绍如何通过使用 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 配置管理器为 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 指定证书来启用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的加密连接。 服务器计算机必须具有提供的证书，客户端计算机必须设置为信任该证书的根颁发机构。 提供是指通过将证书导入 Windows 来安装证书的过程。  
  
 必须颁发证书才能进行 **服务器身份验证**。 证书名称必须为计算机的完全限定域名 (FQDN)。  
  
 用户的证书存储在本地计算机上。 若要安装证书以供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用，必须使用具有本地管理员权限的帐户运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器。

 客户端必须能够验证服务器所用证书的所有权。 如果客户端具有对服务器证书进行签名的证书颁发机构所颁发的公钥证书，则不需要进一步的配置。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 包含多个证书颁发机构所颁发的公钥证书。 如果服务器证书由公共或私人证书颁发机构进行签名，而客户端没有该机构颁发的公钥证书，则必须安装对服务器证书进行签名的证书颁发机构所颁发的公钥证书。  
  
> [!NOTE]  
> 若要在故障转移群集中使用加密，必须在故障转移群集的所有节点上安装带有虚拟服务器的完全限定 DNS 名称的服务器证书。 例如，如果有一个包含两个分别名为 test1.*\<your company>*.com 和 test2.*\<your company>*.com 节点的群集，还有一个名为 virtsql 的虚拟服务器，则需要在这两个节点上安装 virtsql.*\<your company>*.com 的证书。 可以将“ForceEncryption”选项的值设置为“是”。

> [!NOTE]
> 当在 Azure VM 上创建从 Azure Search 索引器到 SQL Server 的加密连接时，请参阅 [在 Azure VM 上配置从 Azure Search 索引器到 SQL Server 的连接](https://azure.microsoft.com/documentation/articles/search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers/)。 

## <a name="certificate-requirements"></a>证书要求

若要让 SQL Server 加载 SSL 证书，证书必须满足以下条件：

- 证书必须位于本地计算机证书存储或当前用户证书存储中。
- SQL Server 服务帐户必须拥有访问 SSL 证书所必需的权限。
- 当前系统时间必须晚于证书的“有效起始时间”属性，并早于证书的“有效截止时间”属性。
- 该证书必须用于服务器身份验证。 这就要求，证书的“增强型密钥使用”属性必须指定“服务器身份验证(1.3.6.1.5.5.7.3.1)”。
- 必须使用 AT_KEYEXCHANGE 的 KeySpec 选项创建证书。 证书的密钥使用属性 (KEY_USAGE) 通常还包括密钥加密 (CERT_KEY_ENCIPHERMENT_KEY_USAGE)。
- 证书的“使用者”属性必须指明，证书公用名称 (CN) 与服务器计算机的主机名或完全限定的域名 (FQDN) 相同。 如果 SQL Server 是在故障转移群集中运行，证书公用名称必须与虚拟服务器的主机名或 FQDN 一致，并且必须在故障转移群集的所有节点上都预配证书。
- SQL Server 2008 R2 和 SQL Server 2008 R2 Native Client 支持通配符证书。 其他客户端可能不支持通配符证书。 有关详细信息，请参阅客户端文档和 [KB258858](http://support.microsoft.com/kb/258858)。

## <a name="to-provision-install-a-certificate-on-the-server"></a>在服务器中提供（安装）证书  

> [!NOTE]
> 请参阅[证书管理（SQL Server 配置管理器）](manage-certificates.md)以在单个服务器上添加证书。
  
1. 在“开始”  菜单上，单击“运行” ，并在“打开”  框中键入 **MMC** ，然后单击“确定” 。  
  
2. 在 MMC 控制台的“文件”菜单上，单击“添加/删除管理单元”。  
  
3. 在“添加/删除管理单元”对话框中，单击“添加”。  
  
4. 在“添加独立管理单元”对话框中，单击“证书”，再单击“添加”。  
  
5. 在“证书管理单元”对话框中，单击“计算机帐户”，再单击“完成”。  
  
6. 在“添加独立管理单元”对话框中，单击“关闭”。  
  
7. 在“添加/删除管理单元”对话框中，单击“确定”。  
  
8. 在“证书”管理单元中，依次展开“证书”和“个人”，右键单击“证书”，指向“所有任务”，然后单击“导入”。  

9. 右键单击导入的证书，指向“所有任务”，然后单击“管理私钥”。 在“安全”对话框中，为 SQL Server 服务帐户使用的用户帐户添加读取权限。  
  
10. 完成 **证书导入向导**，将证书添加到计算机中，然后关闭 MMC 控制台。 有关向计算机添加证书的详细信息，请参阅 Windows 文档。  
  
## <a name="to-provision-install-a-certificate-across-multiple-servers"></a>在多个服务器之间预配（安装）证书

> [!NOTE]
> 请参阅[证书管理（SQL Server 配置管理器）](manage-certificates.md)以在多个服务器之间添加证书。

## <a name="to-export-the-server-certificate"></a>导出服务器证书  
  
1. 在“证书”管理单元中的“证书” / “个人”文件夹中找到证书，右键单击“证书”，指向“所有任务”，然后单击“导出”。  
  
2. 完成 **“证书导出向导”**，将证书文件存储在方便的位置。  
  
## <a name="to-configure-the-server-to-force-encrypted-connections"></a>将服务器配置为强制使用加密连接的具体步骤  
  
1. 在“SQL Server 配置管理器”中，展开“SQL Server 网络配置”右键单击“\<server instance> 的协议”，然后选择“属性”。  
  
2. 在“\<instance name> 属性的协议”对话框中的“证书”选项卡上，从“证书”框的下拉菜单中选择所需证书，然后单击“确定”。  
  
3. 在 **“标志”** 选项卡的 **“ForceEncryption”** 框中，选择 **“是”**，然后单击 **“确定”** 关闭该对话框。  
  
4. 重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务。  

> [!NOTE]
> 要确保客户端和服务器之间的安全连接，请将客户端配置为请求加密连接。 [本文稍后部分](#to-configure-the-client-to-request-encrypted-connections)将介绍更多详细信息。

### <a name="wildcard-certificates"></a>通配符证书

从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 开始，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 支持通配符证书。 其他客户端可能不支持通配符证书。 有关详细信息，请参阅客户端文档。 无法使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager 选择通配符证书。 要使用通配符证书，必须编辑 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQLServer\SuperSocketNetLib` 注册表项，并为“证书”值输入证书的指纹（不留空格）。  

> [!WARNING]  
> [!INCLUDE[ssnoteregistry_md](../../includes/ssnoteregistry-md.md)]  

## <a name="to-configure-the-client-to-request-encrypted-connections"></a>将客户端配置为请求加密连接  

1. 将原始证书或导出的证书文件复制到客户端计算机。  
  
2. 在客户端计算机上，使用“证书”管理单元来安装根证书或导出的证书文件。  
  
3. 在控制台窗格中，右键单击“SQL Server Native Client 配置”，再单击“属性”。  
  
4. 在 **“标志”** 选项卡的 **“强制协议加密”** 框中，单击 **“是”**。  
  
## <a name="to-encrypt-a-connection-from-sql-server-management-studio"></a>通过 SQL Server Management Studio 加密连接  
  
1. 在对象资源管理器工具栏上，单击 **“连接”**，再单击 **“数据库引擎”**。  
  
2. 在 **“连接到服务器”** 对话框中，填写连接信息，然后单击 **“选项”**。  
  
3. 在 **“连接属性”** 选项卡上，单击 **“加密连接”**。  
  
## <a name="see-also"></a>另请参阅

[针对 Microsoft SQL Server 的 TLS 1.2 支持](https://support.microsoft.com/kb/3135244)