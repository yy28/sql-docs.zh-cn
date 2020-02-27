---
title: 在 Active Directory 模式下部署
titleSuffix: SQL Server Big Data Cluster
description: 了解如何在 Active Directory 域中升级 SQL Server 大数据群集。
author: NelGson
ms.author: negust
ms.reviewer: mikeray
ms.date: 02/13/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bd8e571417e7b2171dc135e986fa77f1f0eff089
ms.sourcegitcommit: 10ab8d797a51926e92aec977422b1ee87b46286d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/21/2020
ms.locfileid: "77544872"
---
# <a name="deploy-big-data-clusters-2019-in-active-directory-mode"></a>在 Active Directory 模式下部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文档介绍如何在 Active Directory 身份验证模式下部署 SQL Server 2019 大数据群集 (BDC)，该模式将使用现有 AD 域进行身份验证。

## <a name="background"></a>背景

要启用 Active Directory (AD) 身份验证，BDC 会自动创建群集中各种服务所需的用户、组、计算机帐户和服务主体名称 (SPN)。 要提供对这些帐户的某些控制并允许范围权限，请在部署期间指定一个组织单位 (OU)，其中将创建所有与 BDC 相关的 AD 对象。 在群集部署之前创建此 OU。

要在 Active Directory 中自动创建所有必需对象，BDC 需要在部署过程中使用 AD 帐户。 此帐户需要具有在提供的 OU 中创建用户、组和计算机帐户的权限。

以下步骤假设已有一个 Active Directory 域控制器。 如果没有域控制器，以下[指南](https://social.technet.microsoft.com/wiki/contents/articles/37528.create-and-configure-active-directory-domain-controller-in-azure-windows-server.aspx)包含可提供帮助的步骤。

## <a name="create-ad-objects"></a>创建 AD 对象

在部署具有 AD 集成的 BDC 之前，请执行以下操作：

1. 创建一个将在其中存储所有 BDC AD 对象的组织单位 (OU)。 还可以选择在部署时指定现有 OU。
1. 为 BDC 创建 AD 帐户或使用现有帐户，并向此 BDC AD 帐户提供正确的权限。

### <a name="create-a-user-in-ad-for-bdc-domain-service-account"></a>为 BDC 域服务帐户在 AD 中创建用户

大数据群集需要具有特定权限的帐户。 在继续操作之前，请确保已有 AD 帐户或创建一个新帐户，大数据群集可以使用该帐户来设置必要的对象。

若要在 AD 中创建新用户，可以右键单击域或 OU，然后选择“新建” > “用户”   ：

![image12](./media/deploy-active-directory/image12.png)

此用户在本文中将称为 BDC 域服务帐户  。

### <a name="creating-an-ou"></a>创建 OU

在域控制器上，打开“Active Directory 用户和计算机”  。 在左侧面板上，右键单击要在其下创建 OU 的目录，然后选择“新建”\>“组织单位”，然后按照向导中的提示创建 OU  。 或者，可以使用 PowerShell 创建 OU：

```powershell
New-ADOrganizationalUnit -Name "<name>" -Path "<Distinguished name of the directory you wish to create the OU in>"
```

在本文的示例中，我们将 OU 命名为：`bdc`

![image13](./media/deploy-active-directory/image13.png)

![image14](./media/deploy-active-directory/image14.png)

### <a name="setting-permissions-the-bdc-ad-account"></a>设置 BDC AD 帐户的权限

无论是创建新的 AD 用户还是使用现有的 AD 用户，用户都需要具有某些权限。 此帐户是 BDC 控制器在将群集加入 AD 时将使用的用户帐户。

BDC 域服务帐户 (DSA) 需要能够在 OU 中创建用户、组和计算机帐户。 在下面的步骤中，我们将 BDC 域服务帐户命名为 `bdcDSA`。 你可以为此帐户选择任何名称。

1. 在域控制器上，打开“Active Directory 用户和计算机” 

1. 在左侧面板中，导航到你的域，然后导航到 `bdc` 将使用的 OU

1. 右键单击 OU，然后选择“属性”  。

1. 转到“安全性”选项卡（通过右键单击 OU 并选择“视图”，确保选择“高级功能”   ）

    ![image15](./media/deploy-active-directory/image15.png)

1. 单击“添加...”并添加 [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]DSA 用户  

    ![image16](./media/deploy-active-directory/image16.png)

    ![image17](./media/deploy-active-directory/image17.png)

1. 选择 [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]DSA 用户并清除所有权限，然后单击“高级”  

1. 单击“添加” 

    ![image18](./media/deploy-active-directory/image18.png)

    - 单击“选择主体”，插入 [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]DSA，然后单击“确定”  

    - 将“类型”设置为“允许”  

    - 将“应用对象”设置为“此对象和所有后代对象”  

        ![image19](./media/deploy-active-directory/image19.png)

    - 向下滚动到底部并单击“全部清除” 

    - 滚动回到顶部，然后选择：
       - “读取所有属性” 
       - “写入所有属性” 
       - “创建计算机对象” 
       - “删除计算机对象” 
       - “创建组对象” 
       - “删除组对象” 
       - “创建用户对象” 
       - “删除用户对象” 

    - 单击 **“确定”**

- 单击“添加” 

    - 单击“选择主体”，插入 [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]DSA，然后单击“确定”  

    - 将“类型”设置为“允许”  

    - 将“应用对象”设置为“后代计算机对象”  

    - 向下滚动到底部并单击“全部清除” 

    - 滚动回到顶部，然后选择“重置密码” 

    - 单击 **“确定”**

- 单击“添加” 

    - 单击“选择主体”，插入 [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]DSA，然后单击“确定”  

    - 将“类型”设置为“允许”  

    - 将“应用对象”设置为“后代用户对象”  

    - 向下滚动到底部并单击“全部清除” 

    - 滚动回到顶部，然后选择“重置密码” 

    - 单击 **“确定”**

- 再单击“确定”两次以关闭打开的对话框 

## <a name="prepare-deployment"></a>准备部署

要部署具有 AD 集成的 BDC，需要提供一些附加信息以在 AD 中创建与 BDC 相关的对象。

通过使用 `kubeadm-prod` 配置文件，你将自动获得 AD 集成所需的安全相关信息和终结点相关信息的占位符。

此外，还需要提供 [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)] 将用于在 AD 中创建必要对象的凭据。 这些凭据作为环境变量提供。

## <a name="set-security-environment-variables"></a>设置安全环境变量

以下环境变量提供 BDC 域服务帐户的凭据，该帐户将用于设置 AD 集成。 BDC 还使用此帐户来维护与 BDC 相关的 AD 对象。

```bash
export DOMAIN_SERVICE_ACCOUNT_USERNAME=<AD principal account name>
export DOMAIN_SERVICE_ACCOUNT_PASSWORD=<AD principal password>
```

## <a name="provide-security-and-endpoint-parameters"></a>提供安全参数和终结点参数

除了凭据的环境变量外，还需要提供安全信息和终结点信息，以便 AD 集成正常工作。 所需参数自动属于 `kubeadm-prod` [部署配置文件](deployment-guidance.md#configfile)。

AD 集成需要以下参数。 使用本文后面显示的 `config replace` 命令将这些参数添加到 `control.json` 和 `bdc.json` 文件中。 以下所有示例都使用示例域 `contoso.local`。

- `security.activeDirectory.ouDistinguishedName`：组织单位 (OU) 的可分辨名称，其中将添加群集部署创建的所有 AD 帐户。 如果域名为 `contoso.local`，则 OU 可分辨名称为：`OU=BDC,DC=contoso,DC=local`。

- `security.activeDirectory.dnsIpAddresses`：域控制器的 IP 地址列表

- `security.activeDirectory.domainControllerFullyQualifiedDns`设置用户帐户 ：域控制器的 FQDN 列表。 FQDN 包含域控制器的计算机/主机名。 如果有多个域控制器，可以在此处提供列表。 示例： `HOSTNAME.CONTOSO.LOCAL`

- `security.activeDirectory.realm` 可选参数  ：大多数情况下，领域等同于域名。 对于领域不同于域名的情况，请使用此参数定义领域名称（例如 `CONTOSO.LOCAL`）。

- `security.activeDirectory.domainDnsName`设置用户帐户 ：域的名称（例如 `contoso.local`）。

- `security.activeDirectory.clusterAdmins`设置用户帐户 ：此参数采用一个 AD 组  。 此组的成员将在群集中获得管理员权限。 这意味着他们将在 SQL Server 中具有 sysadmin 权限、在 HDFS 中具有超级用户权限、在控制器中具有管理员权限。 **请注意，在部署开始之前，此组需要存在于 AD 中。另请注意，在 Active Directory 中不能将此组的作用域设置为 DomainLocal。域本地作用域组将导致部署失败。**

- `security.activeDirectory.clusterUsers`设置用户帐户 ：大数据群集中常规用户（无管理员权限）的 AD 组列表。 **请注意，在部署开始之前，这些组需要存在于 AD 中。另请注意，在 Active Directory 中不能将这些组的作用域设置为 DomainLocal。域本地作用域组将导致部署失败。**

- `security.activeDirectory.appOwners` 可选参数  ：有权创建、删除和运行任何应用程序的 AD 组列表。 **请注意，在部署开始之前，这些组需要存在于 AD 中。另请注意，在 Active Directory 中不能将这些组的作用域设置为 DomainLocal。域本地作用域组将导致部署失败。**

- `security.activeDirectory.appReaders` 可选参数：有权运行任何应用程序的 AD 组的列表  。 **请注意，在部署开始之前，这些组需要存在于 AD 中。另请注意，在 Active Directory 中不能将这些组的作用域设置为 DomainLocal。域本地作用域组将导致部署失败。**

**如何查看 AD 组作用域：** 
[单击此处获取说明](https://docs.microsoft.com/powershell/module/activedirectory/get-adgroup?view=winserver2012-ps&viewFallbackFrom=winserver2012r2-ps)，以便查看 AD 组作用域以及确定其是否为 DomainLocal.

如果尚未初始化部署配置文件，则可以运行此命令来获取配置的副本。

```bash
azdata bdc config init --source kubeadm-prod  --target custom-prod-kubeadm
```

要在 `control.json` 文件中设置上述参数，请使用以下 `azdata` 命令。 这些命令将替换配置并在部署之前提供你自己的值。

 > [!IMPORTANT]
 > 在 SQL Server 2019 CU2 版本中，部署配置文件中的安全配置部分的结构发生了明显的变化，并且所有 Active Directory 相关设置安全地位于 control.json 文件的 JSON 树的新 activeDirectory 中    。

下面的示例基于使用 SQL Server 2019 CU2 的情况。 该实例演示了如何替换部署配置中与 AD 相关的参数值。下面的域详细信息为示例值。

```bash
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.ouDistinguishedName=OU\=bdc\,DC\=contoso\,DC\=local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.dnsIpAddresses=[\"10.100.10.100\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.domainControllerFullyQualifiedDns=[\"HOSTNAME.CONTOSO.LOCAL\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.domainDnsName=contoso.local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.clusterAdmins=[\"bdcadminsgroup\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.clusterUsers=[\"bdcusersgroup\"]"
#Example for providing multiple clusterUser groups: [\"bdcusergroup1\",\"bdcusergroup2\"]
```

同样，在 SQL Server 2019 CU2 之前的版本中，你可以运行：

```bash
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.ouDistinguishedName=OU\=bdc\,DC\=contoso\,DC\=local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.dnsIpAddresses=[\"10.100.10.100\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.domainControllerFullyQualifiedDns=[\"HOSTNAME.CONTOSO.LOCAL\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.domainDnsName=contoso.local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.clusterAdmins=[\"bdcadminsgroup\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.clusterUsers=[\"bdcusersgroup\"]"
#Example for providing multiple clusterUser groups: [\"bdcusergroup1\",\"bdcusergroup2\"]
```

除了上述信息之外，还需要提供不同群集终结点的 DNS 名称。 在部署时，将自动在 DNS 服务器中创建使用提供的 DNS 名称的 DNS 条目。 在连接到不同群集终结点时，将使用这些名称。 例如，如果 SQL 主实例的 DNS 名称是 `mastersql`，则将使用 `mastersql.contoso.local,31433` 从工具连接到主实例。

> [!NOTE]
> 请确保在 DNS 服务器中为以下定义的名称创建 DNS 条目。 例如，对于 `kubeadm` 部署，可以在创建 DNS 条目时使用 Kubernetes 主节点的 IP 地址。

```bash
# DNS names for BDC services
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.spec.endpoints[0].dnsName=<controller DNS name>.contoso.local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.spec.endpoints[1].dnsName=<monitoring services DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.master.spec.endpoints[0].dnsName=<SQL Master Primary DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.master.spec.endpoints[1].dnsName=<SQL Master Secondary DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.gateway.spec.endpoints[0].dnsName=<Gateway (Knox) DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.appproxy.spec.endpoints[0].dnsName=<app proxy DNS name>.<Domain name. e.g. contoso.local>"
```

可以在此处找到示例脚本，用于[在具有 AD 集成的单节点 Kubernetes 群集 (kubeadm) 上部署 SQL Server 大数据群集](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu-single-node-vm-ad)。

现在，你应该已设置所有所需的参数，用于部署具有 Active Directory 集成的 BDC。

有关如何部署 [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)] 的完整文档，请访问 [官方文档](deployment-guidance.md)。

## <a name="verify-reverse-dns-entry-for-domain-controller"></a>验证域控制器的反向 DNS 条目

请确保在 DNS 服务器中注册了域控制器本身的反向 DNS 条目（PTR 记录）。 可以通过在域控制器上运行域名 `nslookup` 来验证这一点，以查看是否可以将其解析为域控制器 IP 地址。

## <a name="connect-to-cluster-endpoints-in-ad-mode"></a>以 AD 模式连接到群集终结点

通过 AD 身份验证登录 SQL Server 主实例。

要验证与 SQL Server 实例的 AD 连接，请使用 `sqlcmd` 连接到 SQL 主实例。 部署时，会自动为提供的组创建登录名（`clusterUsers` 和 `clusterAdmins`）。

如果使用的是 Linux，请先以 AD 用户身份运行 `kinit`，然后运行 `sqlcmd`。 如果使用的是 Windows，则只需以所需用户身份从已加入域的客户端计算机登录  。

### <a name="connect-to-master-instance-from-linuxmac"></a>从 Linux/Mac 连接到主实例

```bash
kinit <username>@<domain name>
sqlcmd -S <DNS name for master instance>,31433 -E
```

### <a name="connect-to-master-instance-from-windows"></a>从 Windows 连接到主实例

```cmd
sqlcmd -S <DNS name for master instance>,31433 -E
```

### <a name="log-in-to-sql-server-master-instance-using-azure-data-studio-or-ssms"></a>使用 Azure Data Studio 或 SSMS 登录到 SQL Server 主实例

从已加入域的客户端，可以打开 SSMS 或 Azure Data Studio，并连接到主实例。 这与使用 AD 身份验证连接到任何 SQL Server 实例的体验相同。

从 SSMS：

![image23](./media/deploy-active-directory/image23.png)

从 Azure Data Studio：

![image24](./media/deploy-active-directory/image24.png)}

### <a name="log-in-to-controller-with-ad-authentication"></a>通过 AD 身份验证登录到控制器

#### <a name="connect-to-controller-with-ad-authentication-from-linuxmac"></a>通过 AD 身份验证从 Linux/Mac 连接到控制器

可以使用 `azdata` 和 AD 身份验证连接到控制器终结点。

```bash
kinit <username>@<domain name>
azdata login -e https://<controller DNS name>:30080 --auth ad
```

#### <a name="connect-to-controller-with-ad-authentication-from-windows"></a>通过 AD 身份验证从 Windows 连接到控制器

```cmd
azdata login -e https://<controller DNS name>:30080 --auth ad
```

### <a name="use-ad-authentication-to-knox-gateway-webhdfs"></a>对 Knox 网关使用 AD 身份验证 (webHDFS)

还可以通过 Knox 网关终结点使用 curl 发出 HDFS 命令。 这需要对 Knox 进行 AD 身份验证。 以下 curl 命令通过 Knox 网关发出 webHDFS REST 调用，以创建名为 `products` 的目录

```bash
curl -k -v --negotiate -u : https://<Gateway DNS name>:30443/gateway/default/webhdfs/v1/products?op=MKDIRS -X PUT
```

## <a name="known-issues-and-limitations"></a>已知问题和限制

在此版本中需要注意的限制： 

- 目前，“日志搜索”仪表板和“指标”仪表板不支持 AD 身份验证。 计划在将来的版本中对此终结点提供 AD 支持。 部署时设置的基本用户名和密码可用于对这些仪表板进行身份验证。 所有其他群集终结点都支持 AD 身份验证。

- 安全 AD 模式现在仅适用于 `kubeadm` 部署环境，而不适用于 AKS。 默认情况下，`kubeadm-prod` 部署配置文件包含安全部分。

- 目前，每个域只能使用一个 BDC。 计划在将来的版本中对每个域启用多个 BDC。

- 无法将安全配置中指定的任何 AD 组的作用域设置为 DomainLocal。 可以按照[这些说明](https://docs.microsoft.com/powershell/module/activedirectory/get-adgroup?view=winserver2012-ps&viewFallbackFrom=winserver2012r2-ps)来查看 AD 组的作用域。
