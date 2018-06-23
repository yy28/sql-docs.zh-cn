---
title: 在虚拟机环境中使用内存中 OLTP |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 27ec7eb3-3a24-41db-aa65-2f206514c6f9
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: ac5bae341711dc0ded20efdf57fe1ac776ec208b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024634"
---
# <a name="using-in-memory-oltp-in-a-vm-environment"></a>在虚拟机环境下使用内存中 OLTP
  服务器虚拟化可以帮助你改进应用程序配置、维护、可用性和备份/恢复流程，进而降低 IT 资本和运营成本并提高 IT 效率。 由于近年来的技术进步，可以更轻松地使用虚拟化来合并复杂的数据库工作负载。 本主题说明了在虚拟化环境中使用 [!INCLUDE[hek_1](../includes/hek-1-md.md)] 的最佳做法。  
  
##  <a name="bkmk_memoryPreAllocation"></a> 内存预分配  
 对于虚拟化环境中的内存，更好的性能和增强的支持是两个重要的注意事项。 您必须能够根据不同虚拟机的要求（高峰负载和非高峰负载）快速将内存分配到虚拟机，同时确保不浪费内存。 通过 Hyper-V 动态内存功能，可以更灵活地在主机上运行的虚拟机之间分配和管理内存。  
  
 当虚拟化带有内存优化表的数据库时，需要修改一些用于虚拟化和管理 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的最佳做法。 对于不带有内存优化表的数据库，可遵循两个最佳做法：  
  
-   如果使用 MIN_SERVER_MEMORY，最好只分配需要的内存量，以便保留足够内存以用于其他进程（从而避免分页）。  
  
-   不要将内存预先分配值设置得过高。 否则，其他进程可能无法在需要时获得足够内存，这可能会导致内存分页。  
  
 如果在数据库带有内存优化表时遵循上述做法，尝试还原和恢复数据库可能会导致数据库处于“恢复挂起”状态，即使你拥有可恢复数据库的足够内存时也是如此。 原因在于，与动态内存分配功能将内存分配至数据库相比， [!INCLUDE[hek_2](../includes/hek-2-md.md)] 在启动时以更主动的方式将数据存入内存。  
  
 **解决方法**  
  
 要缓解此问题，请将足够内存预先分配至数据库以恢复或重新启动数据库，而不要分配最小值，依靠动态内存在需要时分配更多内存。  
  
## <a name="see-also"></a>请参阅  
 [内存中 OLTP（内存中优化）](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  