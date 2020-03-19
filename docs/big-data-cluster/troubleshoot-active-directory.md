---
title: 对 Active Directory 模式部署进行故障排除
titleSuffix: SQL Server Big Data Cluster
description: 对在 Active Directory 域中部署 SQL Server 大数据群集进行故障排除。
author: rl-msft
ms.author: rafidl
ms.reviewer: mikeray
ms.date: 03/12/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5d887eadd021641241516a1478c6ac13e0d0bdec
ms.sourcegitcommit: d1f6da6f0f5e9630261cf733c64958938a3eb859
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2020
ms.locfileid: "79191208"
---
# <a name="troubleshoot-sql-server-big-data-cluster-active-directory-mode-deployment"></a>对 SQL Server 大数据群集 Active Directory 模式部署进行故障排除

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍了如何对在 Active Directory 模式下部署 SQL Server 大数据群集进行故障排除。

## <a name="check-deployment-progress"></a>查看部署进度

部署可能需要几分钟的时间。 如果在 15 分钟后群集未就绪，请查看控制器日志以了解更多详细信息。

部署群集时，请检查 Pod。

```console
kubectl get pods -n mssql-cluster
```

验证返回的 Pod 列表是否包括：

- `compute-`$
- `data-`
- `storage-`

如果未创建计算、数据和存储 Pod，请查看日志以找出原因。

## <a name="check-logs"></a>检查日志

若要确定部署退出而没有创建计算、数据或存储 pod 的原因，请查看以下日志： 

- 检查 (`controller.log``<folderOfDebugCopyLog>\debuglogs-mssql-cluster-20200219-093941\mssql-cluster\control-<suffix>\controller\controller\<date>\controller.log`)。 查找以下条目：

  `WARN | StatefulSet master is not ready with 0 ready pods and 3 unready pods `

- 检查 `master-0` `provisioner.log` (`<folderOfDebugCopyLog>\debuglogs-mssql-cluster-20200219-093941\mssql-cluster\master-0\mssql-server\provisioner\provisioner.log`)

  ```
  ERROR | Failed to create sql login for domain user [<domain>.<top-level-domain>\<domain-group>]
    Traceback (most recent call last):
      File "/opt/provisioner/bin/scripts/provisioningpool.py", line 214, in executeNonQueries
        connection.execute_non_query(command)
      File "src/_mssql.pyx", line 1033, in _mssql.MSSQLConnection.execute_non_query
      File "src/_mssql.pyx", line 1061, in _mssql.MSSQLConnection.execute_non_query
      File "src/_mssql.pyx", line 1634, in _mssql.check_and_raise
      File "src/_mssql.pyx", line 1683, in _mssql.maybe_raise_MSSQLDatabaseException
    _mssql.MSSQLDatabaseException: (15401, b"Windows NT user or group '<domain>.<top-level-domain>\\<domain-group>' not found. Check the name again.DB-Lib error message 20018, severity 16:\nGeneral SQL Server error: Check messages from the SQL Server\n")
  WARNING | [3/3] Provisioning exception occurred during provisioning step: ProvisioningMasterPool.
  WARNING | Failed to create sql login for domain user [<domain>.<top-level-domain>\<domain-group>]
  WARNING | Retrying.
  ```

  在上面的示例中，由于域组的范围设置为本地域，因此部署无法为域用户创建登录名。 使用范围设置为全球域或通用域的组。 [在 Active Directory 模式下部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deploy-active-directory.md) 说明了 AD 组范围要求。

## <a name="check-the-scope-of-domain-groups"></a>检查域组的范围。

检查域组 (<`domain-group`>) 的范围。 使用 [get-adgroup](/powershell/module/addsadministration/get-adgroup/)。

如果 `<domain-group>` 组范围是本地域 (`DomainLocal`)，则部署失败。 

下面的 PowerShell 脚本检查名为 `bdcadmins` 和 `bdcusers` 的两个 AD 组的范围。 将名称替换为你的组的名称。 

```powershell
#Administrators and users AD groups
$Cluster_admins_group='bdcadmins'
$Cluster_users_group='bdcusers'

#Performing AD Group Checks...

#AD admin group Check
$ClusterAdminGroupScope_Result = New-Object System.Collections.ArrayList
try {
    $GroupScope = Get-ADgroup -Identity $Cluster_admins_group | Select-Object -ExpandProperty GroupScope
    
    if ($GroupScope -eq 'DomainLocal') {
        [void]$ClusterAdminGroupScope_Result.Add("Misconfiguration - $Cluster_admins_group Group scope is $GroupScope, this scope is not supported, Please change group scope to either Global or Univesal") 
    }
    else {
        [void]$ClusterAdminGroupScope_Result.Add("OK - $Cluster_admins_group Group scope is $GroupScope")
    }
}
catch {
    [void]$ClusterAdminGroupScope_Result.Add("Error - " + $_.exception.message)
}
#Ad users group check
$ClusterUsersGroupScope_Result = New-Object System.Collections.ArrayList
$GroupScope = ''
try {
    $GroupScope = Get-ADgroup -Identity $Cluster_users_group | Select-Object -ExpandProperty GroupScope
    
    if ($GroupScope -eq 'DomainLocal') {
        [void]$ClusterUsersGroupScope_Result.Add("Misconfiguration - $Cluster_users_group Group scope is $GroupScope, this scope is not supported, Please change group scope to either Global or Univesal")
    } 
    else 
    { [void]$ClusterUsersGroupScope_Result.Add("OK - $Cluster_users_group Group scope is $GroupScope") }
}
catch {
    [void]$ClusterUsersGroupScope_Result.Add("Error - " + $_.exception.message)
}

#Display the results
$ClusterUsersGroupScope_Result
```

## <a name="check-security-support-container"></a>检查安全支持容器 

查看安全支持容器日志。

以下命令收集命名空间 `mssql-cluster` 的群集中的安全支持日志。

```console
azdata bdc debug copy-logs -n mssql-cluster -c security-support
```

提取日志并找到 `\mssql-cluster\control-<identifier>\controller\control-rts5t-controller-stdout.log`。

在日志中查找以下条目：

```
ERROR    | Failed to create AD user account 'cntrl-controller'. Error code: 53. Message: Failed to create user object: Failed to add object 'CN=cntrl-controller,OU=bdc, DC=CONTOSO, DC=com' to '  <domain>.<top-level-domain>  ': Server is unwilling to perform. 
ERROR | Failed to create AD user account 'ldap-user'. Error code: 53. Message: Failed to create user object: Failed to add object 'CN=ldap-user,OU=bdc, DC=CONTOSO, DC=com' to '  <domain>.<top-level-domain>  ': Server is unwilling to perform. 
ERROR | Failed to create AD user account 'nginx-mgmtproxy'. Error code: 53. Message: Failed to create user object: Failed to add object 'CN=nginx-mgmtproxy,OU=bdc, DC=CONTOSO, DC=com' to '  <domain>.<top-level-domain>  ': Server is unwilling to perform.
```

当域控制器 DNS 服务器缺少反向 DNS 条目（PTR 记录）时，可能会出现这些条目。

## <a name="verify-reverse-lookup-ptr-record"></a>验证反向查找（PTR 记录）
    
运行以下 PowerShell 脚本以确认是否配置了反向 DNS 条目（PTR 记录）。

```powershell
#Domain Controller FQDN 'DCserver01.contoso.local'
$Domain_controller_FQDN = 'DCserver01.contoso.local'

#Performing Domain Controller DNS record, reverse PTR Checks...
$DcControllerDnsPtr_Result = New-Object System.Collections.ArrayList
try {
    $Domain_controller_DNS_Record = Resolve-DnsName $Domain_controller_FQDN -Type A -Server $Domain_DNS_IP_address -ErrorAction Stop
    foreach ($ip in $Domain_controller_DNS_Record.IPAddress) {
        #resolving hostname by IP address to make sure we have reverse PTR record 
        if ((Resolve-DnsName $ip).NameHost -eq $Domain_controller_FQDN) {
            [void]$DcControllerDnsPtr_Result.add("OK - $Domain_controller_FQDN has an A record with an IP $ip, Reverse PTR record is in place") 
        }
        else {
            [void]$DcControllerDnsPtr_Result.add("Missing - $Domain_controller_FQDN has an A record with an IP $ip, But no reverse PTR record was found for the host")
        }
    }
}
catch {
    [void]$DcControllerDnsPtr_Result.add("Error - " + $_.exception.message)
}

#show the results 
$DcControllerDnsPtr_Result
```

[验证域控制器的反向 DNS 条目（PTR 记录）](deploy-active-directory.md#verify-reverse-dns-entry-for-domain-controller)。