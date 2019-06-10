---
title: 使用 Active Directory 身份验证 (Kerberos)
titleSuffix: Azure Data Studio
description: 了解如何启用 Kerberos 要用于 Azure Data Studio 的 Active Directory 身份验证
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: meet-bhagdev
ms.author: meetb
manager: jroth
ms.openlocfilehash: 4836b22d9903b05d70170aad53fde7ac7101f537
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66778375"
---
# <a name="connect-includename-sosincludesname-sos-shortmd-to-your-sql-server-using-windows-authentication---kerberos"></a>连接[!INCLUDE[name-sos](../includes/name-sos-short.md)]到 SQL Server 使用 Windows 身份验证的 Kerberos 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 连接到 SQL Server 使用 Kerberos 的支持。

若要在 macOS 或 Linux 上使用集成身份验证 （Windows 身份验证），您需要设置**Kerberos 票证**将当前用户链接到 Windows 域帐户。 

## <a name="prerequisites"></a>必要條件

- 访问 Windows 已加入域的计算机才能查询在 Kerberos 域控制器。
- SQL Server 应配置为允许 Kerberos 身份验证。 对于 Unix 上运行的客户端驱动程序，集成身份验证是仅支持使用 Kerberos。 设置 Sql Server 使用 Kerberos 进行身份验证的详细信息可在[此处](https://support.microsoft.com/help/319723/how-to-use-kerberos-authentication-in-sql-server)。 应为每个想要连接到 Sql Server 实例注册 Spn。 列出的 SQL Server Spn 格式的详细信息[此处](https://technet.microsoft.com/library/ms191153%28v=sql.105%29.aspx#SPN%20Formats)


## <a name="checking-if-sql-server-has-kerberos-setup"></a>正在检查 Sql Server 是否有 Kerberos 设置

登录到 Sql Server 的主机。 从 Windows 命令提示符处使用`setspn -L %COMPUTERNAME%`若要列出主机的所有服务主体名称。 应会看到开头 MSSQLSvc/HostName.Domain.com 这意味着 Sql Server 已注册 SPN，并且已准备好接受 Kerberos 身份验证的条目。 
- 如果您不能访问 Sql Server 的主机，然后从任何其他 Windows OS 加入相同 Active Directory，可以使用命令`setspn -L <SQLSERVER_NETBIOS>`< SQLSERVER_NETBIOS > 其中是 Sql Server 的主机的计算机名称。


## <a name="get-the-kerberos-key-distribution-center"></a>获取 Kerberos 密钥分发中心

查找 Kerberos KDC （密钥分发中心） 配置值。 在加入到 Active Directory 域的 Windows 计算机上运行以下命令： 

启动`cmd.exe`并运行`nltest`。

```
nltest /dsgetdc:DOMAIN.COMPANY.COM (where "DOMAIN.COMPANY.COM" maps to your domain's name)

Sample Output
DC: \\dc-33.domain.company.com
Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
...
The command completed successfully
```
复制是必需的 KDC 配置值，在此事例的 dc 33.domain.company.com DC 名称

## <a name="join-your-os-to-the-active-directory-domain-controller"></a>将您的操作系统加入到 Active Directory 域控制器

### <a name="ubuntu"></a>Ubuntu
```bash
sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
```

编辑`/etc/network/interfaces`文件，以便你的 AD 域控制器的 IP 地址被列为 dns 名称服务器。 例如： 

```/etc/network/interfaces
<...>
# The primary network interface
auth eth0
iface eth0 inet dhcp
dns-nameservers **<AD domain controller IP address>**
dns-search **<AD domain name>**
```

> [!NOTE]
> 对于不同的计算机，网络接口 (eth0) 可能会有所不同。 若要确定使用哪一个，请运行 ifconfig 并复制具有一个 IP 地址和传输和接收的字节数的接口。

编辑此文件之后，重启网络服务：

```bash
sudo ifdown eth0 && sudo ifup eth0
```

现在检查你`/etc/resolv.conf`文件包含类似于以下行：  

```Code
nameserver **<AD domain controller IP address>**
```

```bash
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
* Success
```
   
### <a name="redhat-enterprise-linux"></a>RedHat Enterprise Linux
```bash
sudo yum install realmd krb5-workstation
```

编辑`/etc/sysconfig/network-scripts/ifcfg-eth0`文件 （或其他界面配置文件根据需要），以便你的 AD 域控制器的 IP 地址列出 DNS 服务器：

```/etc/sysconfig/network-scripts/ifcfg-eth0
<...>
PEERDNS=no
DNS1=**<AD domain controller IP address>**
```

编辑此文件之后，重启网络服务：

```bash
sudo systemctl restart network
```

现在检查你`/etc/resolv.conf`文件包含类似于以下行：  

```Code
nameserver **<AD domain controller IP address>**
```

```bash
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
* Success
   
```

### <a name="macos"></a>macOS

- 通过执行以下步骤在 macOS 加入 Active Directory 域控制器：



## <a name="configure-kdc-in-krb5conf"></a>Krb5.conf 中配置 KDC

编辑`/etc/krb5.conf`在所选的编辑器中。 配置下列密钥

```bash
sudo vi /etc/krb5.conf

[libdefaults]
  default_realm = DOMAIN.COMPANY.COM
 
[realms]
DOMAIN.COMPANY.COM = {
   kdc = dc-33.domain.company.com
}
```

然后保存 krb5.conf 文件并退出

> [!NOTE]
> 域必须全部大写


## <a name="test-the-ticket-granting-ticket-retrieval"></a>测试票证授予票证检索

获取票证授予票证 (TGT) 从 KDC。

```bash
kinit username@DOMAIN.COMPANY.COM
```

查看可用的票证使用 kinit。 如果 kinit 成功，应看到一个票证。 

```bash
klist

krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM.
```

## <a name="connect-using-includename-sosincludesname-sos-shortmd"></a>使用连接 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

* 创建新的连接配置文件

* 选择**Windows 身份验证**作为身份验证类型

* 完成连接配置文件中，单击**连接**

成功连接后，你的服务器显示在*服务器*侧栏。
