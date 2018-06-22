---
title: 运行系统监视器 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- System Monitor [SQL Server], running
- Windows System Monitor [SQL Server], running
- remote procedure calls [SQL Server]
- starting Windows NT System Monitor
- RPC
ms.assetid: 05297984-bc8d-43df-829c-032387f7ea61
caps.latest.revision: 21
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 53e6fa6b09523bd03e4fbad8e9ae40248e738c78
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016329"
---
# <a name="run-system-monitor"></a>运行系统监视器
  系统监视器使用远程过程调用 (RPC) 从 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]收集信息。 拥有运行系统监视器的 Microsoft Windows 权限的任何用户都可以使用系统监视器来监视 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
> [!NOTE]  
>  使用系统监视器或性能监视器时，不能连接到运行于 Windows 98 上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
 与所有性能监视工具一样，使用系统监视器监视 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时，性能方面会受到一些影响。 特定实例中的实际影响取决于硬件平台、计数器数量以及所选更新间隔。 但是，将系统监视器与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 集成可以尽量减少对性能的影响。  
  
> [!NOTE]  
>  如果选择了系统监视器管理单元中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 性能计数器进行监视，即使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 未运行，也会看到计数器。  
  
 有关启动系统监视器的信息，请参阅[启动系统监视器 (Windows)](../performance/start-system-monitor-windows.md)。  
  
  