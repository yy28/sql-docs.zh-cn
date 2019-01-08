---
title: 配置 FailureConditionLevel 属性设置 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 513dd179-9a46-46da-9fdd-7632cf6d0816
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 705b1a8438e4d8d4d193c30d0237467ea977abda
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53374999"
---
# <a name="configure-failureconditionlevel-property-settings"></a>配置 FailureConditionLevel 属性设置
  使用 FailureConditionLevel 属性可以设置 AlwaysOn 故障转移群集实例 (FCI) 进行故障转移或重新启动的条件。 对此属性的更改会立即应用，而无需重新启动 Windows Server 故障转移群集 (WSFC) 服务或 FCI 资源。  
  
-   **开始之前：**[FailureConditionLevel 属性设置](#Restrictions)，[安全](#Security)  
  
-   **若要配置 FailureConditionLevel 属性设置，请使用** [PowerShell](#PowerShellProcedure)、[故障转移群集管理器](#WSFC)、[Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> FailureConditionLevel 属性设置  
 针对递增的级别设置故障条件。 对于级别 1-5，每个级别除了自己的条件外，还包括之前级别的所有条件。 这意味着，每个级别越大，故障转移或重新启动的几率不断加大。  有关详细信息，请参阅 [Failover Policy for Failover Cluster Instances](failover-policy-for-failover-cluster-instances.md) 主题的“确定故障”一节。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 需要 ALTER SETTINGS 和 VIEW SERVER STATE 权限。  
  
##  <a name="PowerShellProcedure"></a> 使用 PowerShell  
  
##### <a name="to-configure-failureconditionlevel-settings"></a>配置 FailureConditionLevel 设置  
  
1.  通过 **“以管理员身份运行”** 启动提升的 Windows PowerShell。  
  
2.  导入 `FailoverClusters` 模块以启用群集 cmdlet。  
  
3.  使用`Get-ClusterResource`cmdlet 查找[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]资源，然后使用`Set-ClusterParameter`cmdlet，以设置**FailureConditionLevel**故障转移群集实例的属性。  
  
> [!TIP]  
>  每次您打开新的 PowerShell 窗口时，都需要导入 `FailoverClusters` 模块。  
  
### <a name="example-powershell"></a>示例 (PowerShell)  
 下面的示例将 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 资源“`SQL Server (INST1)`”上的 FailureConditionLevel 设置更改为在出现严重服务器错误时执行故障转移或重新启动。  
  
```powershell  
Import-Module FailoverClusters  
  
$fci = "SQL Server (INST1)"  
Get-ClusterResource $fci | Set-ClusterParameter FailureConditionLevel 3  
  
```  
  
### <a name="related-content-powershell"></a>相关内容 (PowerShell)  
  
-   [群集和高可用性](https://blogs.msdn.com/b/clustering/archive/2009/05/23/9636665.aspx) （故障转移群集和网络负载平衡团队博客）  
  
-   [故障转移群集上的 Windows PowerShell 入门](https://technet.microsoft.com/library/ee619762\(WS.10\).aspx)  
  
-   [群集资源命令和等效的 Windows PowerShell cmdlet](https://msdn.microsoft.com/library/ee619744.aspx#BKMK_resource)  
  
##  <a name="WSFC"></a> 使用故障转移群集管理器管理单元  
 **配置 FailureConditionLevel 属性设置：**  
  
1.  打开故障转移群集管理器管理单元。  
  
2.  展开 **“服务和应用程序”** ，然后选择 FCI。  
  
3.  右键单击“其他资源”下的“SQL Server 资源”，然后从菜单中选择“属性”。 此时将打开 SQL Server 资源 **“属性”** 对话框。  
  
4.  选择 **“属性”** 选项卡，为 **FaliureConditionLevel** 属性输入所需的值，然后单击 **“确定”** 以应用更改。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **配置 FailureConditionLevel 属性设置：**  
  
 使用 [ALTER SERVER CONFIGURATION](/sql/t-sql/statements/alter-server-configuration-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句，可指定 FailureConditionLevel 属性值。  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
 以下示例将 FailureConditionLevel 属性设置为 0，表示对于任何故障条件将不自动触发故障转移或重新启动。  
  
```  
ALTER SERVER CONFIGURATION SET FAILOVER CLUSTER PROPERTY FailureConditionLevel = 0;  
```  
  
## <a name="see-also"></a>请参阅  
 [sp_server_diagnostics (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql)   
 [Failover Policy for Failover Cluster Instances](failover-policy-for-failover-cluster-instances.md)  
  
  
