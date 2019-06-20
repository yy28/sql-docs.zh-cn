---
title: 配置 HealthCheckTimeout 属性设置 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 3bbeb979-e6fc-4184-ad6e-cca62108de74
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: acb2a812f2e3c29a56916c671d76d91c676272d6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63049491"
---
# <a name="configure-healthchecktimeout-property-settings"></a>配置 HealthCheckTimeout 属性设置
  HealthCheckTimeout 设置用于指定的时间，以毫秒为单位，SQL Server 资源 DLL 应等待返回的信息[sp_server_diagnostics](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql)报告之前存储过程AlwaysOn 故障转移群集实例 (FCI) 为不响应。 对超时设置所做的更改会立即生效，不需要重新启动 SQL Server 资源。  
  
-   **开始之前：** [限制和局限](#Limits)、[安全性](#Security)  
  
-   **若要配置 HeathCheckTimeout 设置，请使用：** [PowerShell](#PowerShellProcedure)，[故障转移群集管理器](#WSFC)， [Transact SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Limits"></a> 限制和局限  
 此属性的默认值为 60,000 毫秒（60 秒）。 最小值为 15,000 毫秒（15 秒）。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要 ALTER SETTINGS 和 VIEW SERVER STATE 权限。  
  
##  <a name="PowerShellProcedure"></a> 使用 PowerShell  
  
##### <a name="to-configure-healthchecktimeout-settings"></a>配置 HealthCheckTimeout 设置  
  
1.  通过 **“以管理员身份运行”** 启动提升的 Windows PowerShell。  
  
2.  导入 `FailoverClusters` 模块以启用群集 cmdlet。  
  
3.  使用`Get-ClusterResource`cmdlet 查找[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]资源，然后使用`Set-ClusterParameter`cmdlet，以设置**HealthCheckTimeout**故障转移群集实例的属性。  
  
> [!TIP]  
>  每次您打开新的 PowerShell 窗口时，都需要导入 `FailoverClusters` 模块。  
  
### <a name="example-powershell"></a>示例 (PowerShell)  
 下面的示例将 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 资源“`SQL Server (INST1)`”上的 HealthCheckTimeout 设置更改为 60000 毫秒。  
  
```powershell  
Import-Module FailoverClusters  
  
$fci = "SQL Server (INST1)"  
Get-ClusterResource $fci | Set-ClusterParameter HealthCheckTimeout 60000  
  
```  
  
### <a name="related-content-powershell"></a>相关内容 (PowerShell)  
  
-   [群集和高可用性](https://blogs.msdn.com/b/clustering/archive/2009/05/23/9636665.aspx) （故障转移群集和网络负载平衡团队博客）  
  
-   [故障转移群集上的 Windows PowerShell 入门](https://technet.microsoft.com/library/ee619762\(WS.10\).aspx)  
  
-   [群集资源命令和等效的 Windows PowerShell cmdlet](https://msdn.microsoft.com/library/ee619744.aspx#BKMK_resource)  
  
##  <a name="WSFC"></a> 使用故障转移群集管理器管理单元  
 **配置 HealthCheckTimeout 设置**  
  
1.  打开故障转移群集管理器管理单元。  
  
2.  展开 **“服务和应用程序”** ，然后选择 FCI。  
  
3.  右键单击“其他资源”  下的“SQL Server 资源”  ，然后从右键菜单中选择“属性”  。 此时将打开 SQL Server 资源 **“属性”** 对话框。  
  
4.  选择 **“属性”** 选项卡，为 **HealthCheckTimeout** 属性输入所需的值，然后单击 **“确定”** 以应用更改。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 使用 [ALTER SERVER CONFIGURATION](/sql/t-sql/statements/alter-server-configuration-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句，你可以指定 HealthCheckTimeOut 属性值。  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
 下面的示例将 HealthCheckTimeout 选项设置为 15,000 毫秒（15 秒）。  
  
```  
ALTER SERVER CONFIGURATION   
SET FAILOVER CLUSTER PROPERTY HealthCheckTimeout = 15000;  
```  
  
## <a name="see-also"></a>请参阅  
 [故障转移群集实例的故障转移策略](failover-policy-for-failover-cluster-instances.md)  
  
  
