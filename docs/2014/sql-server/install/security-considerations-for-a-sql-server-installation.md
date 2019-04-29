---
title: 安装 SQL Server 的安全注意事项 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- firewall systems [SQL Server]
- server message blocks [SQL Server]
- disabling protocols
- security [SQL Server], installations
- protocols [SQL Server], disabling
- NetBIOS [SQL Server]
- services [SQL Server], security
- SMB [SQL Server]
- isolating services [SQL Server]
- Setup [SQL Server], security
- low SQL Server installation privileges
- NTFS [SQL Server]
- physical security [SQL Server]
- file system security [SQL Server]
- installing SQL Server, security
ms.assetid: cf96155f-30a8-48b7-8d6b-24ce90dafdc7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: eec38b5ecc524f0d3decd02c0832efd1909e8f00
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63127894"
---
# <a name="security-considerations-for-a-sql-server-installation"></a>安装 SQL Server 的安全注意事项
  安全对于每个产品和每家企业都很重要。 遵循简单的最佳做法，可以避免很多安全漏洞。 本主题讨论安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 前和安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之后应考虑采用的一些最佳安全做法。 功能的参考主题中包括了特定功能的安全指南。  
  
## <a name="before-installing-includessnoversionincludesssnoversion-mdmd"></a>安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 设置服务器环境时，请遵循以下最佳做法：  
  
-   [增强物理安全性](#physical_security)  
  
-   [使用防火墙](#firewalls)  
  
-   [隔离服务](#isolated_services)  
  
-   [配置安全的文件系统](#sa_with_least_privileges)  
  
-   [禁用 NetBIOS 和服务器消息块](#disabled_protocols)  
  
-   [在域控制器上安装 SQL Server](../../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md#Install_DC)  
  
###  <a name="physical_security"></a> Enhance Physical Security  
 物理和逻辑隔离是构成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安全的基础。 若要增强 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装的物理安全性，请执行以下任务：  
  
-   将服务器置于专门的房间，未经授权的人员不得入内。  
  
-   将数据库的宿主计算机置于受物理保护的场所，最好是上锁的机房，房中配备水灾检测和火灾检测监视系统或灭火系统。  
  
-   将数据库安装在公司 Intranet 的安全区域中，并且不得将 SQL Server 直接连接到 Internet。  
  
-   定期备份所有数据，并将备份存储在远离工作现场的安全位置。  
  
###  <a name="firewalls"></a> Use Firewalls  
 防火墙对于协助确保 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装的安全十分重要。 若要使防火墙发挥最佳效用，请遵循以下指南：  
  
-   在服务器和 Internet 之间放置防火墙。 启用防火墙。 如果防火墙处于关闭状态，请将其开启。 如果防火墙处于开启状态，请不要将其关闭。  
  
-   将网络分成若干安全区域，区域之间用防火墙分隔。 先阻塞所有通信流量，然后有选择地只接受所需的通信。  
  
-   在多层环境中，使用多个防火墙创建屏蔽子网。  
  
-   如果在 Windows 域内部安装服务器，请将内部防火墙配置为允许使用 Windows 身份验证。  
  
-   如果应用程序使用分布式事务处理，可能必须要将防火墙配置为允许 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分布式事务处理协调器 (MS DTC) 在不同的 MS DTC 实例之间进行通信。 还需要将防火墙配置为允许在 MS DTC 和资源管理器（如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]）之间进行通信。  
  
 有关默认 Windows 防火墙设置的详细信息，以及有关影响 [!INCLUDE[ssDE](../../includes/ssde-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]和 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]的 TCP 端口的说明，请参阅 [配置 Windows 防火墙以允许 SQL Server 访问](../../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)。  
  
###  <a name="isolated_services"></a> Isolate Services  
 隔离服务可以降低风险，防止已受到危害的服务被用于危及其他服务。 若要隔离服务，请考虑以下原则：  
  
-   在不同的 Windows 帐户下运行各自的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务。 对每个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务，尽可能使用不同的低权限 Windows 或本地用户帐户。 有关详细信息，请参阅 [配置 Windows 服务帐户和权限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)预览版本升级问题的解答。  
  
###  <a name="sa_with_least_privileges"></a> Configure a Secure File System  
 使用正确的文件系统可提高安全性。 对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装，应执行以下几项任务：  
  
-   使用 NTFS 文件系统 (NTFS)。 NTFS 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装的首选文件系统，因为它比 FAT 文件系统更加稳定和更容易恢复。 NTFS 还可以使用安全选项，例如文件和目录访问控制列表 (ACL) 和加密文件系统 (EFS) 文件加密。 在安装期间，如果检测到 NTFS， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将对注册表项和文件设置相应的 ACL。 不应对这些权限做任何更改。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的未来版本可能不支持在具有 FAT 文件系统的计算机上进行安装。  
  
    > [!NOTE]  
    >  如果使用 EFS，则将在运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的帐户的标识下加密数据库文件。 只有此帐户才可解密文件。 如果必须更改运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的帐户，则应先在旧帐户下解密文件，然后在新帐户下将文件重新加密。  
  
-   对关键数据文件使用独立磁盘冗余阵列 (RAID)。  
  
###  <a name="disabled_protocols"></a> Disable NetBIOS and Server Message Block  
 外围网络中的服务器应禁用所有不必要的协议，包括 NetBIOS 和服务器消息块 (SMB)。  
  
 NetBIOS 使用以下端口：  
  
-   UDP/137（NetBIOS 名称服务）  
  
-   UDP/138（NetBIOS 数据报服务）  
  
-   TCP/139（NetBIOS 会话服务）  
  
 SMB 使用以下端口：  
  
-   TCP/139  
  
-   TCP/445  
  
 Web 服务器和域名系统 (DNS) 服务器不需要 NetBIOS 或 SMB。 在这些服务器上，禁用这两个协议可以减轻由用户枚举带来的威胁。  
  
###  <a name="Install_DC"></a> 在域控制器上安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 出于安全方面的考虑，我们建议您不要将 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装在域控制器上。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序不会阻止在作为域控制器的计算机上进行安装，但存在以下限制：  
  
-   在域控制器上，无法在本地服务帐户下运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务。  
  
-   将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装到计算机上之后，无法将此计算机从域成员更改为域控制器。 必须先卸载 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，然后才能将主机计算机更改为域控制器。  
  
-   将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装到计算机上之后，无法将此计算机从域控制器更改为域成员。 必须先卸载 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，然后才能将主机计算机更改为域成员。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集实例。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序不能在只读域控制器上创建安全组或预配 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户。 在这种情况下，安装将失败。  
  
## <a name="during-or-after-installation-of-includessnoversionincludesssnoversion-mdmd"></a>在安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 安装完成后，若要增强所安装的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 软件的安全性，请遵循以下有关帐户和身份验证模式的最佳做法：  
  
 **服务帐户**  
  
-   使用尽可能低的权限运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务。  
  
-   将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务与低特权 Windows 本地用户帐户或域用户帐户相关联。  
  
-   有关详细信息，请参阅 [配置 Windows 服务帐户和权限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)预览版本升级问题的解答。  
  
 **身份验证模式**  
  
-   连接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时要求 Windows 身份验证。  
  
-   使用 Kerberos 身份验证。 有关详细信息，请参阅 [为 Kerberos 连接注册服务主体名称](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)。  
  
 **强密码**  
  
-   始终为 `sa` 帐户分配强密码。  
  
-   始终启用密码策略检查来验证密码强度以及密码是否过期。  
  
-   始终对所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名使用强密码。  
  
> [!IMPORTANT]  
>  在安装 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 过程中，为 BUILTIN\Users 组添加一个登录名。 这可以使计算机的所有通过身份验证的用户作为 public 角色成员访问 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 实例。 可以安全地删除 BUILTIN\Users 登录名，以限制 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 对具有单独登录名或为使用此登录名的其他 Windows 组成员的计算机用户的访问。  
  
## <a name="see-also"></a>请参阅  
 [硬件和软件要求安装 SQL Server 2014 的](hardware-and-software-requirements-for-installing-sql-server.md)   
 [网络协议和网络库](../../../2014/sql-server/install/network-protocols-and-network-libraries.md)   
 [为 Kerberos 连接注册服务主体名称](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)  
  
  
