---
title: 内存优化的文件组 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 14106cc9-816b-493a-bcb9-fe66a1cd4630
caps.latest.revision: 15
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 491cd5968109e69f8561b973cf32a6292a9d357d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="the-memory-optimized-filegroup"></a>内存优化的文件组
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  若要创建内存优化表，必须首先创建内存优化的文件组。 内存优化的文件组容纳一个或多个容器。 每个容器都包含数据文件或差异文件，或是同时包含两者。  
  
 即使 SCHEMA_ONLY 表中的数据行未保留，并且内存优化表和本机编译的存储过程中的元数据存储在传统目录中， [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 引擎仍需要 SCHEMA_ONLY 内存优化表的内存优化的文件组来提供针对带内存优化表的数据库的一致体验。  
  
 内存优化的文件组基于文件流文件组，具有以下差异：  
  
-   只能为每个数据库创建一个内存优化的文件组。 您需要将文件组显式标记为包含 memory_optimized_data。 可以在创建数据库时创建文件组，也可以稍后添加文件组：  
  
    ```sql  
    ALTER DATABASE imoltp ADD FILEGROUP imoltp_mod CONTAINS MEMORY_OPTIMIZED_DATA  
    ```  
  
-   需要将一个或多个容器添加到 `MEMORY_OPTIMIZED_DATA` 文件组。 例如：  
  
    ```sql  
    ALTER DATABASE imoltp ADD FILE (name='imoltp_mod1', filename='c:\data\imoltp_mod1') TO FILEGROUP imoltp_mod  
    ```  
  
-   你无需启用文件流（[启用和配置 FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)）来创建内存优化文件组。 通过 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 引擎完成与文件流的映射。  
  
-   可以将新容器添加到内存优化的文件组。 您可能需要新容器来扩展持久内存优化表所需的存储，并跨多个容器分发 IO。  
  
-   在 AlwaysOn 可用性组配置中优化与内存优化文件组相关的数据移动。 与发送到辅助副本的文件流文件不同，内存优化的文件组中的检查点文件（数据文件和差异文件）不会发送到辅助副本。 使用辅助副本上的事务日志构造数据文件和差异文件。  
  
以下是针对内存优化文件组的限制：  
  
-   创建内存优化的文件组后，您只能通过删除数据库来删除它。 在生产环境中，您不太可能需要删除内存优化的文件组。  
  
-   在内存优化的文件组中，您无法删除非空容器或将数据和差异文件对移至另一个容器。  
  
-   无法指定容器的 `MAXSIZE`。  
  
## <a name="configuring-a-memory-optimized-filegroup"></a>配置内存优化的文件组  
 您应考虑在内存优化的文件组中创建多个容器，并在不同的驱动器上分配这些容器以实现更多带宽来将数据流式传输到内存中。  
  
 在配置存储时，您必须提供大小为持久内存优化表大小的四倍的可用磁盘空间。 还必须确保 I/O 子系统支持工作负荷所需的 IOPS。 如果按给定的 IOPS 填充数据和差异文件对，则您需要考虑按 3 倍的 IOPS 来进行存储和合并操作。 可以通过将一个或多个容器添加到内存优化的文件组来增加存储容量和 IOPS。  
  
## <a name="see-also"></a>另请参阅  
 [创建和管理用于内存优化对象的存储](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
 [数据库文件和文件组](../../relational-databases/databases/database-files-and-filegroups.md) 
  
