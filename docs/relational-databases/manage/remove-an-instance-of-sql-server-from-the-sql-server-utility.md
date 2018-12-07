---
title: 从 SQL Server 实用工具中删除 SQL Server 实例 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.utility.remove.f1
ms.assetid: ae1d126a-46d2-47bf-b339-17c743df6491
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7db64758c57b586982a2f2edfa2008dbec164f90
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52535224"
---
# <a name="remove-an-instance-of-sql-server-from-the-sql-server-utility"></a>从 SQL Server 实用工具中删除 SQL Server 实例
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  使用以下步骤从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中删除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例。 此过程从 UCP 列表视图中删除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例，并且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具数据收集将停止。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例不卸载。  
  
> [!IMPORTANT]  
>  在您使用此过程从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中删除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例前，请确保 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 SQL Server 代理服务正在要删除的实例上运行。  
  
1.  从 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的实用工具资源管理器中，单击 **“托管实例”**。 观察实用工具资源管理器内容窗格中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例的列表视图。  
  
2.  在该列表视图的 **“SQL Server 实例名称”** 列中，选择要从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具删除的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 右键单击要删除的实例，然后选择“删除托管实例…”。  
  
3.  为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例指定具有管理员权限的凭据：单击“连接…”，验证“连接到服务器”对话框中的信息，然后单击“连接”。 您将在 **“删除托管实例”** 对话框中看到登录信息。  
  
4.  若要确认该操作，请单击 **“确定”**。 若要退出该操作，请单击 **“取消”**。  
  
## <a name="manually-remove-a-managed-instance-of-sql-server-from-a-sql-server-utility"></a>手动从 SQL Server 实用工具中删除 SQL Server 的托管实例  
 此过程从 UCP 列表视图中删除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例并且停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具数据收集。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例不卸载。  
  
 使用 PowerShell 从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中删除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例。 此脚本执行以下操作：  
  
-   按服务器实例名称获取 UCP。  
  
-   从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具中删除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例。  
  
```  
# Get Ucp connection  
$UcpServerInstanceName = "ComputerName\InstanceName";  
$UtilityInstance = new-object -Type Microsoft.SqlServer.Management.Smo.Server $UcpServerInstanceName;  
$UcpConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $UtilityInstance.ConnectionContext.SqlConnectionObject;  
$Utility = [Microsoft.SqlServer.Management.Utility.Utility]::Connect($UcpConnection);  
  
# Now remove the ManagedInstance from the SQL Server Utility  
$ServerInstanceName = "ComputerName\InstanceName";  
$Instance = new-object -Type Microsoft.SqlServer.Management.Smo.Server $ServerInstanceName;  
$InstanceConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $Instance.ConnectionContext.SqlConnectionObject;  
$ManagedInstance = $Utility.ManagedInstances[$ServerInstanceName];  
$ManagedInstance.Remove($InstanceConnection);  
```  
  
 请注意，在引用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例名称时，此名称务必与在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中存储的名称完全相同。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的区分大小写的实例上，必须使用与 @@SERVERNAME 返回的完全一致的大小写来指定实例名称。 若要获取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的托管实例的实例名称，请对该托管实例运行以下查询：  
  
```  
select @@SERVERNAME AS instance_name  
```  
  
 此时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的托管实例将从 UCP 完全删除。 在您下次刷新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实用工具的数据时，该托管实例将从列表视图中消失。 此状态完全等同于用户成功在 SSMS 用户界面中完成删除托管实例操作。  
  
## <a name="see-also"></a>另请参阅  
 [使用实用工具资源管理器管理 SQL Server 实用工具](../../relational-databases/manage/use-utility-explorer-to-manage-the-sql-server-utility.md)   
 [SQL Server 实用工具故障排除](https://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)  
  
  
