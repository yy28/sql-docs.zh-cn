---
title: SQL Server 属性（"AlwaysOn 高可用性" 选项卡） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: d8630923-a600-4f1c-aca1-027453a3ec82
author: mikeraymsft
ms.author: mikeray
manager: craigg
ms.openlocfilehash: daf3ed025405b753116bba267ce6f4c50d350601
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62678456"
---
# <a name="sql-server-properties-alwayson-high-availability-tab"></a>SQL Server 属性（“AlwaysOn 高可用性”选项卡）
  使用 **** 配置管理器的 **“SQL Server 属性”** 对话框中的“AlwaysOn 高可用性” [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 选项卡，可以在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中启用或禁用“AlwaysOn 可用性组”功能。 启用 AlwaysOn 可用性组是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例将可用性组用作高可用性和灾难恢复解决方案的一个先决条件。  
  
##  <a name="Prerequisites"></a>先决条件  
 若要启用 AlwaysOn 可用性组，服务器实例必须满足以下先决条件：  
  
-   该服务器实例必须驻留在 Windows Server 故障转移群集 (WSFC) 节点上。  
  
-   若要位于同一个可用性组中，实例必须位于同一个 WSFC 群集中。 可用性组无法跨越多个 WSFC 群集。  
  
-   服务器实例必须正在运行支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]版本。  
  
-   一次仅为一个服务器实例启用 AlwaysOn 可用性组。 在启用 AlwaysOn 可用性组之后，一直等待，直到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务已重新启动，然后才启用下一个服务器实例。  
  
> [!NOTE]  
>  有关功能支持的信息和有关 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]其他先决条件、局限性和建议的信息，请参阅 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 联机丛书。  
  
## <a name="dialog-options"></a>对话框选项  
 **Windows 故障转移群集名称**  
 显示本地计算机在其中作为一个节点的 WSFC 群集的名称。  
  
 **启用 AlwaysOn 可用性组**  
 使用此复选框可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的这一实例上启用或禁用 AlwaysOn 可用性组，如下所示：  
  
-   如果此复选框为空，则当前禁用 AlwaysOn 可用性组。 若要启用 AlwaysOn 可用性组，请选中此复选框，单击 **“确定”**，然后手动重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务。  
  
-   如果已选中此复选框，则当前启用了 AlwaysOn 可用性组。 若要禁用 AlwaysOn 可用性组，请取消选中此复选框，然后单击 **“确定”**。 这会导致服务器实例重新启动。  
  
    > [!TIP]  
    >  在启用 AlwaysOn 可用性组之后，应从服务器实例中删除任何本地化可用性副本。 如果您删除了给定可用性组的最后一个副本，则还应删除此组。  
  
## <a name="uielement-list"></a>UIElement 列表  
  
> [!NOTE]  
>  有关在禁用 AlwaysOn 可用性组后如何进行操作的详细信息以及如何创建和配置可用性组的信息，请参阅 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 联机丛书。  
  
  
