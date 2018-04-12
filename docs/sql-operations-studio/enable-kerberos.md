---
title: 在连接 SQL Operations Studio (preview) 时使用 Active Directory 身份验证 (Kerberos) |Microsoft 文档
description: 了解如何启用 Kerberos 要用于 SQL Operations Studio (preview) 的 Active Directory 身份验证
ms.custom: tools|sos
ms.date: 11/17/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: article
author: meet-bhagdev
ms.author: meetb
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dbd229a0106506f744074df760ee10f871474ebb
ms.sourcegitcommit: 094c46e7fa6de44735ed0040c65a40ec3d951b75
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="connect-includename-sosincludesname-sos-shortmd-to-your-sql-server-using-windows-authentication---kerberos"></a>连接[!INCLUDE[name-sos](../includes/name-sos-short.md)]到 SQL Server 使用 Windows 身份验证的 Kerberos 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 连接到使用 Kerberos 的 SQL Server 的支持。

若要在 macOS 或 Linux 上使用集成身份验证 （Windows 身份验证），你需要设置**Kerberos 票证**将你当前的用户链接到 Windows 域帐户。 

## <a name="prerequisites"></a>必要條件

- 访问 Windows 已加入域的计算机以便查询 Kerberos 域控制器。
- SQL Server 应配置为允许 Kerberos 身份验证。 对于在 Unix 上运行的客户端的驱动程序的情况下，集成的身份验证只支持使用 Kerberos。 找不到设置 Sql Server 使用 Kerberos 进行身份验证的详细信息[此处](https://support.microsoft.com/en-us/help/319723/how-to-use-kerberos-authentication-in-sql-server)。 应为每个你尝试连接到的 Sql Server 实例注册 Spn。 列出的 SQL Server Spn 格式的详细信息[此处](https://technet.microsoft.com/en-us/library/ms191153%28v=sql.105%29.aspx#SPN%20Formats)


## <a name="checking-if-sql-server-has-kerberos-setup"></a>正在检查 Sql Server 是否有 Kerberos 安装程序

登录到 Sql Server 的主机。 从 Windows 命令提示符下使用`setspn -L %COMPUTERNAME%`可列出主机的所有服务主体名称。 您应看到开头 MSSQLSvc/HostName.Domain.com 这意味着 Sql Server 已注册 SPN 和已准备好接受 Kerberos 身份验证的项。 
- 如果你无权访问的主机的 Sql Server 中，然后从任何其他 Windows 操作系统加入相同 Active Directory，你可以使用命令`setspn -L <SQLSERVER_NETBIOS>`< SQLSERVER_NETBIOS > 其中是 Sql Server 的主机的计算机名称。


## <a name="get-the-kerberos-key-distribution-center"></a>获取 Kerberos 密钥分发中心

查找 Kerberos KDC （密钥分发中心） 配置值。 在加入到 Active Directory 域的 Windows 计算机上运行以下命令： 

启动`cmd.exe`并运行`nltest`。

```
nltest /dsgetdc:DOMAIN.COMPANY.COM (where “DOMAIN.COMPANY.COM” maps to your domain’s name)

Sample Output
DC: \\dc-33.domain.company.com
Address: \\2111:4444:2111:33:1111:ecff:ffff:3333
...
The command completed successfully
```
复制是必需的 KDC 配置值，在此案例的 dc 33.domain.company.com DC 名称

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
> 网络接口 (eth0) 可能因不同的计算机而不同。 若要了解你使用哪一个，运行 ifconfig，并复制有一个 IP 地址和传输和接收的字节的接口。

编辑此文件之后, 重新启动网络服务：

```bash
sudo ifdown eth0 && sudo ifup eth0
```

现在请检查你`/etc/resolv.conf`文件包含如下所示的行：  

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

编辑`/etc/sysconfig/network-scripts/ifcfg-eth0`文件 （或文件根据其他接口配置），以便你的 AD 域控制器的 IP 地址被列为 DNS 服务器：

```/etc/sysconfig/network-scripts/ifcfg-eth0
<...>
PEERDNS=no
DNS1=**<AD domain controller IP address>**
```

编辑此文件之后, 重新启动网络服务：

```bash
sudo systemctl restart network
```

现在请检查你`/etc/resolv.conf`文件包含如下所示的行：  

```Code
nameserver **<AD domain controller IP address>**
```

```bash
sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
<...>
* Success
   
```

### <a name="macos"></a>macOS

- 你 macOS 加入 Active Directory 域控制器通过 [执行以下步骤] (https://support.apple.com/kb/PH26282?viewlocale=en_US&locale=en_US)。



## <a name="configure-kdc-in-krb5conf"></a>在 krb5.conf 中配置 KDC

编辑`/etc/krb5.conf`在所选的编辑器中。 配置以下项

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
> 域必须在全部大写


## <a name="test-the-ticket-granting-ticket-retrieval"></a>测试票证授予票证检索

获取票证授予票证 (TGT) 从 KDC。

```bash
kinit username@DOMAIN.COMPANY.COM
```

查看使用 kinit 可用票证。 如果 kinit 成功，你应看到一个票证。 

```bash
klist

krbtgt/DOMAIN.COMPANY.COM@ DOMAIN.COMPANY.COM.
```

## <a name="connect-using-includename-sosincludesname-sos-shortmd"></a>使用连接 [!INCLUDE[name-sos](../includes/name-sos-short.md)]

* 创建新的连接配置文件

* 选择**Windows 身份验证**作为身份验证类型

* 完成的连接配置文件中，单击**连接**

成功连接后，你的服务器将显示在*服务器*侧栏。
