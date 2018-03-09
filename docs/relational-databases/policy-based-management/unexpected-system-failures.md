---
title: "意外的系统故障 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 1679bf9e-a2ef-4f90-8907-a002f7341a7d
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 57104ed0869aa6916d11d7329d18526cdaa72836
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2018
---
# <a name="unexpected-system-failures"></a>意外的系统故障
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]此规则检查计算机事件日志中是否存在 SYSTEM Event 6008。 该事件表示意外的系统关闭。 系统可能不稳定，并且可能不能提供承载 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例所需的稳定性和完整性。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 立即找出服务器意外重新启动的原因，或者将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例移到另一台计算机。  
  
  
