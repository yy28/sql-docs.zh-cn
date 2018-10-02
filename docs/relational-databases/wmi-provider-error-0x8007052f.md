---
title: WMI 错误 0x8007052f | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- 0x8007052f (WMI error)
ms.assetid: a33f12bd-15c4-42a8-b343-de44c3e87729
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 668cb77d2e15fc23981f6f32bcac44391567f0df
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47810376"
---
# <a name="wmi-provider-error-0x8007052f"></a>WMI 提供程序错误 0x8007052f
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|0x8007052f|  
|事件源|WMI 提供程序错误|  
|组件|SQL Server 配置管理器|  
|符号名称|不适用|  
|消息正文|登录失败: 用户帐户限制。 可能是因为不允许使用空白密码、登录时间限制或者是强制实施策略限制。|  
  
## <a name="explanation"></a>解释  
 当 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 在 Windows Server 群集或 Windows Server 域控制器上运行时，如果使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 配置管理器切换到内置帐户（Network Service、Local Service 或 Local System），则会发生此错误。 请不要在 Windows Server 群集或 Windows Server 域控制器上以内置帐户运行服务。 有关服务帐户的建议，请参阅 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 联机丛书中的“设置 Windows 服务帐户”主题。  
  
## <a name="user-action"></a>用户操作  
 配置 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 以使用域帐户。  
  
  
