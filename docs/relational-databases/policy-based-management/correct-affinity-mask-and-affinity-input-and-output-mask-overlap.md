---
title: 正确的关联掩码和关联输入/输出掩码重叠 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 1a0da6df-57ff-4f3f-aae9-2fbc4897508c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 05652024c7d887e7bc34119f3e529c7f404324bc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47623365"
---
# <a name="correct-affinity-mask-and-affinity-input-and-output-mask-overlap"></a>正确的关联掩码和关联输入/输出掩码重叠
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此规则检查 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例是否有一个或多个要分配以用于 affinity mask 和 affinity I/O mask 选项的处理器。 在有多个处理器的计算机上，affinity mask 和 affinity I/O mask 选项用于指定哪些 CPU 由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用。 启用包含关联掩码和关联 I/O 掩码的 CPU 会由于强制过度使用处理器而降低性能。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 指定 affinity mask 和 affinity I/O mask 选项时，应同时指定这两个选项，但每个 CPU 的启用次数不超过一次。  
  
 请勿在 affinity mask 和 affinity I/O mask 选项中同时启用同一个 CPU。 每个 CPU 对应的位应处于下列三种状态之一：  
  
-   在 affinity mask 和 affinity I/O mask 选项中均为 0  
  
-   在 affinity mask 选项中为 0，在 affinity I/O mask 选项中为 1  
  
-   在 affinity mask 选项中为 1，在 affinity I/O mask 选项中为 0  
  
## <a name="for-more-information"></a>有关详细信息  
 [affinity mask 服务器配置选项](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)  
  
 [affinity I/O mask 服务器配置选项](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md)  
  
 [affinity64 mask 服务器配置选项](../../database-engine/configure-windows/affinity64-mask-server-configuration-option.md)  
  
 [affinity64 I/O mask 服务器配置选项](../../database-engine/configure-windows/affinity64-input-output-mask-server-configuration-option.md)  
  
## <a name="see-also"></a>另请参阅  
 [使用基于策略的管理来监视和强制执行最佳实践](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
