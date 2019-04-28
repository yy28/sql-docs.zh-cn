---
title: 删除可用性组侦听程序 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilitygroup.removeaglistener.default.f1
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
ms.assetid: fd9bba9a-d29f-4c23-8ecd-aaa049ed5f1b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f5c1ee253c6fedde6b0954f36eb115253f876d0b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62789468"
---
# <a name="remove-an-availability-group-listener-sql-server"></a>删除可用性组侦听器 (SQL Server)
  本主题说明如何通过在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)]、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]或 PowerShell 从 AlwaysOn 可用性组中删除可用性组侦听器。  
  
-   **开始之前：**  
  
     [先决条件](#Prerequisites)  
  
     [建议](#Recommendations)  
  
     [安全性](#Security)  
  
-   **删除侦听器，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Prerequisites"></a> 先决条件  
  
-   您必须连接到承载主副本的服务器实例。  
  
###  <a name="Recommendations"></a> 建议  
 在删除可用性组侦听器之前，我们建议您确保没有任何应用程序在使用它。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 对可用性组要求 ALTER AVAILABILITY GROUP 权限、CONTROL AVAILABILITY GROUP 权限、ALTER ANY AVAILABILITY GROUP 权限或 CONTROL SERVER 权限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **删除可用性组侦听器**  
  
1.  在对象资源管理器中，连接到承载主副本的服务器实例，然后单击服务器名称以便展开服务器树。  
  
2.  依次展开 **“AlwaysOn 高可用性”** 节点和 **“可用性组”** 节点。  
  
3.  展开可用性组节点，然后展开 **“可用性组侦听器”** 节点。  
  
4.  右键单击要删除的侦听器，然后选择 **“删除”** 命令。  
  
5.  这将打开 **“从可用性组中删除侦听器”** 对话框。 有关详细信息，请参阅本主题后面的 [从可用性组中删除侦听器](#AgListenerPropertiesDialog)。  
  
###  <a name="AgListenerPropertiesDialog"></a> 从可用性组中删除侦听器（对话框）  
 **名称**  
 要删除的侦听器的名称。  
  
 **结果**  
 将显示一个链接，提示 **“成功”** 或 **“错误”**，可单击该链接查看详细信息。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **删除可用性组侦听器**  
  
1.  连接到承载主副本的服务器实例。  
  
2.  按如下所示使用 [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql) 语句：  
  
     ALTER AVAILABILITY GROUP *group_name* REMOVE LISTENER **'*`dns_name`*'**  
  
     其中， *group_name* 是可用性组的名称， *dns_name* 是可用性组侦听器的 DNS 名称。  
  
     下面的示例将删除 `AccountsAG` 可用性组的侦听器。 DNS 名称为 AccountsAG_Listener。  
  
    ```  
    ALTER AVAILABILITY GROUP AccountsAG REMOVE LISTENER 'AccountsAG_Listener';  
    ```  
  
##  <a name="PowerShellProcedure"></a> 使用 PowerShell  
 **删除可用性组侦听器**  
  
1.  将默认的 (`cd`) 设置为承载主副本的服务器实例。  
  
2.  使用内置的 `Remove-Item` cmdlet 来删除侦听器。 例如，以下命令从名为 `MyListener` 的可用性组中删除名为 `MyAg`的侦听器。  
  
    ```  
    Remove-Item `   
    SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AGListeners\MyListener  
    ```  
  
    > [!NOTE]  
    >  若要查看 cmdlet 的语法，请在 `Get-Help` PowerShell 环境中使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cmdlet。 有关详细信息，请参阅 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)。  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
-   [创建或配置可用性组侦听程序 (SQL Server)](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [查看可用性组侦听程序属性 (SQL Server)](view-availability-group-listener-properties-sql-server.md)  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组概述&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [可用性组侦听程序、客户端连接和应用程序故障转移 (SQL Server)](../../listeners-client-connectivity-application-failover.md)  
  
  
