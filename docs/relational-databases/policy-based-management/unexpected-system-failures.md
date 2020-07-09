---
title: 意外的系统故障 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 1679bf9e-a2ef-4f90-8907-a002f7341a7d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 84fe7ae204c14a0ecaebb3141d4f08175bfee793
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727272"
---
# <a name="unexpected-system-failures"></a>意外的系统故障
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  此规则检查计算机事件日志中是否存在 SYSTEM Event 6008。 该事件表示意外的系统关闭。 系统可能不稳定，并且可能不能提供承载 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例所需的稳定性和完整性。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 立即找出服务器意外重新启动的原因，或者将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例移到另一台计算机。  
  
  
