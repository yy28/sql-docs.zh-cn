---
title: 内存优化的文件组 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 14106cc9-816b-493a-bcb9-fe66a1cd4630
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: e68b94ce70e24d16ac1cc94274b9dac05974dbe7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028129"
---
# <a name="the-memory-optimized-filegroup"></a>内存优化的文件组
  若要创建内存优化表，必须首先创建内存优化的文件组。 内存优化的文件组容纳一个或多个容器。 每个容器都包含数据文件或差异文件，或是同时包含两者。  
  
 即使 SCHEMA_ONLY 表中的数据行未保留，并且内存优化表和本机编译的存储过程中的元数据存储在传统目录中， [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 引擎仍需要 SCHEMA_ONLY 内存优化表的内存优化的文件组来提供针对带内存优化表的数据库的一致体验。  
  
 内存优化的文件组基于文件流文件组，具有以下差异：  
  
-   只能为每个数据库创建一个内存优化的文件组。 您需要将文件组显式标记为包含 memory_optimized_data。 可以在创建数据库时创建文件组，也可以稍后添加文件组：  
  
    ```  
    ALTER DATABASE imoltp ADD FILEGROUP imoltp_mod CONTAINS MEMORY_OPTIMIZED_DATA  
    ```  
  
-   您需要将一个或多个容器添加到 MEMORY_OPTIMIZED_DATA 文件组。 例如：  
  
    ```  
    ALTER DATABASE imoltp ADD FILE (name='imoltp_mod1', filename='c:\data\imoltp_mod1') TO FILEGROUP imoltp_mod  
    ```  
  
-   你无需启用文件流（[启用和配置 FILESTREAM](../blob/enable-and-configure-filestream.md)）来创建内存优化文件组。 通过 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 引擎完成与文件流的映射。  
  
-   可以将新容器添加到内存优化的文件组。 您可能需要新容器来扩展持久内存优化表所需的存储，并跨多个容器分发 IO。  
  
-   在 AlwaysOn 可用性组配置中优化与内存优化的文件组相关的数据移动。 与发送到辅助副本的文件流文件不同，内存优化的文件组中的检查点文件（数据文件和差异文件）不会发送到辅助副本。 使用辅助副本上的事务日志构造数据文件和差异文件。  
  
 以下是内存优化的文件组的限制：  
  
-   创建内存优化的文件组后，您只能通过删除数据库来删除它。 在生产环境中，您不太可能需要删除内存优化的文件组。  
  
-   在内存优化的文件组中，您无法删除非空容器或将数据和差异文件对移至另一个容器。  
  
-   您无法指定容器的 MAXSIZE。  
  
## <a name="configuring-a-memory-optimized-filegroup"></a>配置内存优化的文件组  
 您应考虑在内存优化的文件组中创建多个容器，并在不同的驱动器上分配这些容器以实现更多带宽来将数据流式传输到内存中。  
  
 在配置存储时，您必须提供大小为持久内存优化表大小的四倍的可用磁盘空间。 您还必须确保 IO 子系统支持工作负荷所需的 IOPS。 如果按给定的 IOPS 填充数据和差异文件对，则您需要考虑按 3 倍的 IOPS 来进行存储和合并操作。 可以通过将一个或多个容器添加到内存优化的文件组来增加存储容量和 IOPS。  
  
 在具有多个容器和多个驱动器的情况下，采用循环法将数据和差异文件分配到容器中。 从第一个容器中分配第一个数据文件，并从下一个容器中分配差异文件，随后按此分配模式重复操作。 如果您有奇数个驱动器，并且每个驱动器均映射到一个容器，则此分配方案将跨容器均匀分配数据和差异文件。 但是，如果您有偶数个驱动器，并且每个驱动器均映射到一个容器，则可能会导致存储不均衡，其中数据文件映射到奇数个驱动器，而差异文件映射到偶数个驱动器。 若要在恢复时获得平衡 IO 流，可考虑将数据和差异文件对放在相同的主轴/存储上，如以下示例所述。  
  
 **示例：** 考虑两个容器使用的内存优化文件组： 在驱动器 X 和 Y 的驱动器上的容器 2 上的容器 1。由于数据和差异文件的分配都是在轮循机制方式，容器 1 将只有数据文件和容器 2 只有差异文件，这会导致的不平衡持久性存储，以及每秒，为数据文件的输入/输出操作将显著大于差异文件。 若要在驱动器 X 和 Y 之间均匀分发数据和差异文件，创建而不是两个四个容器，并映射到驱动器 X 和到驱动器 Y 接下来的两个容器的前两个容器。使用轮循机制分配的第一个数据和第一个增量文件将从分配容器 1 和容器 2 分别映射到驱动器 X。同样，将从容器 3 和容器-4 映射到驱动器 Y 分配的下一步的数据和差异文件。这允许将数据和差异文件均匀分布到两个驱动器。  
  
## <a name="see-also"></a>请参阅  
 [创建和管理用于内存优化的对象的存储](creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  