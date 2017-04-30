---
title: "意外的系统故障 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 1679bf9e-a2ef-4f90-8907-a002f7341a7d
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6ea8adc9d59ca0a41a5daf09168ff8e3aa709972
ms.lasthandoff: 04/11/2017

---
# <a name="unexpected-system-failures"></a>意外的系统故障
  此规则检查计算机事件日志中是否存在 SYSTEM Event 6008。 该事件表示意外的系统关闭。 系统可能不稳定，并且可能不能提供承载 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例所需的稳定性和完整性。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 立即找出服务器意外重新启动的原因，或者将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例移到另一台计算机。  
  
  
