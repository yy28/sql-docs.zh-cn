---
title: SQL Server 属性（“AlwaysOn 高可用性”选项卡）
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: d8630923-a600-4f1c-aca1-027453a3ec82
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: d57f7e3f98c9db33569414e3c6876e54503f25bf
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "75306824"
---
# <a name="sql-server-properties-always-on-high-availability-tab"></a>SQL Server 属性（“AlwaysOn 高可用性”选项卡）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  可以使用 **Configuration Manager “SQL Server 属性”对话框中的“AlwaysOn 高可用性”选项卡启用或禁用** 中的“AlwaysOn 可用性组”功能  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 启用 AlwaysOn 可用性组是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例将可用性组用作高可用性和灾难恢复解决方案的一个先决条件。  
  
##  <a name="Prerequisites"></a>先决条件  
 若要启用 AlwaysOn 可用性组，服务器实例必须满足以下先决条件：  
  
-   该服务器实例必须驻留在 Windows Server 故障转移群集 (WSFC) 节点上。  
  
-   若要位于同一个可用性组中，实例必须位于同一个 WSFC 群集中。 可用性组无法跨越多个 WSFC 群集。  
  
-   服务器实例必须正在运行支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]版本。  
  
-   一次仅为一个服务器实例启用 AlwaysOn 可用性组。 在启用 AlwaysOn 可用性组之后，一直等待，直到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务已重启，然后才启用下一个服务器实例。  
  
> [!NOTE]  
>  有关功能支持的信息和有关 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]其他先决条件、局限性和建议的信息，请参阅 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 联机丛书。  
  
## <a name="dialog-options"></a>对话框选项  
 **Windows 故障转移群集名称**  
 显示本地计算机在其中作为一个节点的 WSFC 群集的名称。  
  
 **启用 AlwaysOn 可用性组**  
 使用此复选框可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的这一实例上启用或禁用 AlwaysOn 可用性组，如下所示：  
  
-   如果此复选框为空，则当前禁用了 AlwaysOn 可用性组。 若要启用 AlwaysOn 可用性组，请选中此复选框，单击  “确定”，然后手动重启 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务。  
  
-   如果已选中此复选框，则当前启用了 AlwaysOn 可用性组。 若要禁用 AlwaysOn 可用性组，请取消选中此复选框，然后单击“确定”  。 这会导致服务器实例重新启动。  
  
    > [!TIP]  
    >  禁用 AlwaysOn 可用性组之后，应从服务器实例中删除任何本地可用性副本。 如果您删除了给定可用性组的最后一个副本，则还应删除此组。  
  
## <a name="uielement-list"></a>UIElement 列表  
  
> [!NOTE]  
>  有关在禁用 AlwaysOn 可用性组后如何进行操作的详细信息以及如何创建和配置可用性组的信息，请参阅 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 联机丛书。  
  
  
