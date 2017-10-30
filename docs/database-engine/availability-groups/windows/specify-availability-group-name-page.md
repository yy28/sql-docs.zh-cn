---
title: "“指定可用性组选项”页（新建可用性组向导/添加数据库向导）| Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.newagwizard.specifyagname.f1
- sql13.swb.adddatabasewizard.specifyagname.f1
ms.assetid: dcb6374d-becb-4c6c-b88c-5a8273f8aa38
caps.latest.revision: 13
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4f47049a35bed481329f9ea55ad4fc8d429ff42c
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="specify-availability-group-options-page"></a>“指定可用性组选项”页
  此主题介绍“指定可用性组名称”页中的选项。 [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] 的 [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] 和 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]均使用此主题。  
  
##  <a name="PageOptions"></a>指定可用性组选项  
 **可用性组名称**  
 指定可用性组的名称。 对于新可用性组，请指定在 Windows Server 故障转移群集 (WSFC) 的所有可用性组中唯一的有效 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 标识符。 可用性组名称的最大长度为 128 个字符。  

 群集类型 接下来，指定群集类型。 可能的群集类型取决于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本和操作系统。 从以下列表中选择一个类型：

   * Windows Server 故障转移群集
   
      当可用性组托管在属于 Windows Server 故障转移群集的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的实例上时使用，以实现高可用性和灾难恢复。 适用于所有受支持的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本。 

   * EXTERNAL
      
      当可用性组托管在由外部群集技术（例如 Linux 上的 Pacemaker）管理的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的实例上时使用，以实现高可用性和灾难恢复。 适用于 [!INCLUDE[sssqlv14](../../../includes/sssqlv14-md.md)] 及更高版本。

   * **NONE**
      
      当可用性组托管在不由群集技术管理的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的实例上时使用，以实现读取缩放和负载均衡。 适用于 [!INCLUDE[sssqlv14](../../../includes/sssqlv14-md.md)] 及更高版本。 
 
   数据库级别运行状况检测 勾选此框，为可用性组启用数据库级别运行状况检测 (DB_FAILOVER)。 数据库运行状况检测会说明数据库何时不再处于联机状态、何时出错以及何时触发可用性组的自动故障转移。 请参阅 [SQL Server AlwaysOn 数据库运行状况检测故障转移选项](sql-server-always-on-database-health-detection-failover-option.md)。


Select Databases Page (New Availability Group Wizard and Add Database Wizard)  
  
##  <a name="LaunchWiz"></a> 相关任务  
  
-   [使用“新建可用性组”对话框 (SQL Server Management Studio)](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [使用“将数据库添加到可用性组向导”(SQL Server Management Studio)](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
## <a name="see-also"></a>另请参阅  
 [AlwaysOn 可用性组概述 (SQL Server)](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  

