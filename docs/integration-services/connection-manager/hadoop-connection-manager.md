---
title: Hadoop 连接管理器 | Microsoft Docs
ms.custom: ''
ms.date: 06/29/2020
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hadoopconn.f1
ms.assetid: 8bb15b97-9827-46bc-aca6-068534ab18c4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 93565cbcc0140dd439dc2e7c52880879c6d815ba
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86915093"
---
# <a name="hadoop-connection-manager"></a>Hadoop 连接管理器

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Hadoop 连接管理器通过使用你为属性指定的值使 SQL Server Integration Services (SSIS) 包能够连接到 Hadoop 群集。  
  
## <a name="configure-the-hadoop-connection-manager"></a>配置 Hadoop 连接管理器  
  
1.  在“添加 SSIS 连接管理器”对话框中，选择“Hadoop” > “添加”  。 此时将打开“Hadoop 连接管理器编辑器”  对话框。  
  
2.  若要配置相关的 Hadoop 群集信息，请在左窗格中选择“WebHCat”或“WebHDFS”选项卡 。
  
3.  如果启用“WebHCat”选项以在 Hadoop 上调用 Hive 或 Pig 作业，请执行以下操作： 
  
    1.  对于“WebHCat 主机”，请输入承载 WebHCat 服务的服务器。  
  
    2.  对于“WebHCat 端口” ，请输入 WebHCat 服务的端口，该端口默认是 50111。  
  
    3.  选择访问 WebHCat 服务的  “身份验证”方法。 可用值有“基本”  和 **Kerberos**。  
  
         ![具有基本身份验证的 Hadoop 连接管理器编辑器的屏幕截图](../../integration-services/connection-manager/media/hadoop-cm-basic.png "具有基本身份验证的 Hadoop 连接管理器编辑器")  
  
         ![具有 Kerberos 身份验证的 Hadoop 连接管理器编辑器的屏幕截图](../../integration-services/connection-manager/media/hadoop-cm-kerberos.png "具有 Kerberos 身份验证的 Hadoop 连接管理器编辑器")  
  
    4.  对于“WebHCat 用户” ，请输入有权访问 WebHCat 的“用户”  。  
  
    5.  如果你选择 **Kerberos** 身份验证，请输入用户的“密码”  和“域” 。  
  
4.  如果启用“WebHDFS”选项以从 HDFS 中复制数据或将数据复制到其中，请执行以下操作： 
  
    1.  对于“WebHDFS 主机” ，请输入承载 WebHDFS 服务的服务器。  
  
    2.  对于“WebHDFS 端口” ，请输入 WebHDFS 服务的端口，该端口默认是 50070。  
  
    3.  选择访问 WebHDFS 服务的  “身份验证”方法。 可用值有“基本”  和 **Kerberos**。  
  
    4.  对于“WebHDFS 用户” ，请输入有权访问 HDFS 的用户。  
  
    5.  如果你选择 **Kerberos** 身份验证，请输入用户的“密码”  和“域” 。  
  
5.  选择“测试连接”。 （仅测试你启用的连接）。  
  
6.  选择“确定”以关闭该对话框。  

## <a name="connect-with-kerberos-authentication"></a>连接 Kerberos 身份验证
有两个选项可用来设置本地环境，以便可以配合使用 Kerberos 身份验证和 Hadoop 连接管理器。 可选择更符合你情况的选项。
-   选项 1：[将 SSIS 计算机联接到 Kerberos 领域](#kerberos-join-realm)
-   选项 2：[启用 Windows 域和 Kerberos 领域之间的相互信任](#kerberos-mutual-trust)

### <a name="option-1-join-the-ssis-computer-to-the-kerberos-realm"></a><a name="kerberos-join-realm"></a>方法 1：将 SSIS 计算机联接到 Kerberos 领域

#### <a name="requirements"></a>要求：

-   网关计算机需要联接 Kerberos 领域，且不能联接任何 Windows 域。

#### <a name="how-to-configure"></a>配置方式：

在 SSIS 计算机上：

1.  运行 Ksetup 实用工具来配置 Kerberos 密钥发行中心 (KDC) 服务器和领域。

    计算机必须配置为工作组的成员，因为 Kerberos 领域与 Windows 域不同。 设置 Kerberos 领域并添加 KDC 服务器，如以下示例所示。 根据需要，将 `REALM.COM` 替换为各自的领域。

    ```console
    C:> Ksetup /setdomain REALM.COM`
    C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
    ```

    运行上述命令后，重启计算机。

2.  使用 Ksetup 命令验证配置。 输出应如以下示例所示：

    ```console
    C:> Ksetup
    default realm = REALM.COM (external)
    REALM.com:
        kdc = <your_kdc_server_address>
    ```

### <a name="option-2-enable-mutual-trust-between-the-windows-domain-and-the-kerberos-realm"></a><a name="kerberos-mutual-trust"></a>方法 2：启用 Windows 域和 Kerberos 领域之间的相互信任

#### <a name="requirements"></a>要求：
-   网关计算机必须联接 Windows 域。
-   需要用于更新域控制器设置的权限。

#### <a name="how-to-configure"></a>配置方式：

> [!NOTE]
> 根据需要，将下面教程中的 `REALM.COM` 和 `AD.COM` 替换为各自的领域和域控制器。

在 KDC 服务器上：

1.  编辑 krb5.conf 文件中的 KDC 配置。 通过引用下面的配置模板，允许 KDC 信任 Windows 域。 默认情况下，配置位于 /etc/krb5.conf。

    ```console
    [logging]
    default = FILE:/var/log/krb5libs.log
    kdc = FILE:/var/log/krb5kdc.log
    admin_server = FILE:/var/log/kadmind.log

    [libdefaults]
    default_realm = REALM.COM
    dns_lookup_realm = false
    dns_lookup_kdc = false
    ticket_lifetime = 24h
    renew_lifetime = 7d
    forwardable = true

    [realms]
    REALM.COM = {
        kdc = node.REALM.COM
        admin_server = node.REALM.COM
        }
    AD.COM = {
        kdc = windc.ad.com
        admin_server = windc.ad.com
        }

    [domain_realm]
    .REALM.COM = REALM.COM
    REALM.COM = REALM.COM
    .ad.com = AD.COM
    ad.com = AD.COM

    [capaths]
    AD.COM = {
        REALM.COM = .
        }
    ```

    在配置后重新启动 KDC 服务。

2.  在 KDC 服务器上准备名为“krbtgt/REALM\@AD.COM”的主体。 使用以下命令：

    `Kadmin> addprinc krbtgt/REALM.COM@AD.COM`

3.  在 **hadoop.security.auth_to_local** HDFS 服务配置文件中，添加 `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`。

在域控制器上：

1.  运行以下 Ksetup 命令以添加一个领域条目：

    ```console
    C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
    C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM
    ```

2.  建立从 Windows 域到 Kerberos 领域的信任。 在下面的示例中，`[password]` 是主体 krbtgt/REALM.COM\@AD.COM 的密码。

    `C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /password:[password]`

3.  选择要与 Kerberos 一起使用的加密算法。

    1. 转到“服务器管理器” > “组策略管理” > “域”  。 从此处转到“组策略对象” > “默认或活动的域策略” > “编辑”  。

    2. 在“组策略管理编辑器”弹出窗口中，转到“计算机配置” > “策略” > “Windows 设置”   。 从此处转到“安全设置” > “本地策略” > “安全选项”  。 配置“网络安全:配置 Kerberos 允许的加密类型”。

    3. 选择想要用来连接到 KDC 的加密算法。 通常，可以选择任一选项。

        ![Kerberos 加密类型的屏幕截图](media/hadoop-connection-manager/config-encryption-types-for-kerberos.png)

    4. 使用 Ksetup 命令指定用于特定领域的加密算法。

        `C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96`

4.  若要在 Windows 域中使用 Kerberos 主体，请创建域帐户和 Kerberos 主体之间的映射。

    1. 转到“管理工具” > “Active Directory 用户和计算机” 。

    2. 通过选择“视图” > “高级功能”，配置高级功能 。

    3. 找到要创建映射的帐户，右键单击以查看“名称映射”，然后选择“Kerberos 名称”选项卡 。

    4. 从领域中添加主体。

        ![“安全身份映射”对话框的屏幕截图](media/hadoop-connection-manager/map-security-identity.png)

在网关计算机上：

运行以下 Ksetup 命令以添加一个领域条目。

```console
C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM
```

## <a name="see-also"></a>另请参阅  
 [Hadoop 配置单元任务](../../integration-services/control-flow/hadoop-hive-task.md)   
 [Hadoop Pig 任务](../../integration-services/control-flow/hadoop-pig-task.md)   
 [Hadoop 文件系统任务](../../integration-services/control-flow/hadoop-file-system-task.md)  
  
  
