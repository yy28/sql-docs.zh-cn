---
title: 全文搜索升级选项 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- Full-Text Search
- Upgrade options, Full-Text Search
ms.assetid: 16c9376b-5fbb-4495-a429-06a2493849c9
caps.latest.revision: 18
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: af3bf4f26b94e6fc8ce18c07ed052ef53087f68c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138125"
---
# <a name="full-text-search-upgrade-options"></a>全文搜索升级选项
  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装向导的“全文搜索升级选项”页选择用于此时要升级的数据库的全文搜索升级选项。  
  
 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中，每个全文检索都驻留在属于文件组的全文目录中，它们均具有物理路径，并被视为数据库文件。 现在，全文目录是表示一组全文检索的逻辑概念，即虚拟对象。 因此，新的全文目录不会视为带有物理路径的数据库文件。 但是，在升级包含数据文件的所有全文目录期间，将在相同磁盘上创建新的文件组。 这可以在升级后维护旧磁盘的 I/O 行为。 该目录的所有全文检索均被放置到新的文件组中（如果存在根路径）。 如果旧的全文目录路径无效，该升级则将全文检索保留在与基表相同的文件组中，或者保留在主文件组中（对于分区表）。  
  
## <a name="options"></a>“常规”  
 升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]时，请选择下列全文升级选项之一。  
  
 **导入**  
 导入全文目录。 一般情况下，导入速度比重新生成速度要快很多。 例如，当仅使用一个 CPU 时，导入的运行速度比重新生成要快 10 倍左右。 不过，从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 导入的全文目录不能使用新的和增强的断字符，因此最终可能还是要重新生成全文目录。  
  
> [!NOTE]  
>  重新生成可以以多线程模式运行，如果可用的 CPU 在 10 个以上，且您允许重新生成操作使用所有这些 CPU，则重新生成操作的运行速度可能比导入更快。  
  
 如果全文目录不可用，则会重新生成关联的全文检索。 此选项仅对 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 数据库可用。  
  
 有关导入全文检索的影响的信息，请参阅本主题后面的“有关选择全文升级选项的注意事项”。  
  
 **Rebuild**  
 使用新的和增强的断字符重新生成全文目录。 重新生成索引可能需要许多时间，且升级后可能需要占用大量的 CPU 和内存。  
  
 **重置**  
 重置全文目录。 从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]升级时，将删除全文目录文件，但会保留全文目录和全文检索的元数据。 在进行升级后，所有全文检索将禁用更改跟踪，并且不会自动启动爬网。 在升级完成后，目录将保留为空，直至手动执行完全填充。  
  
 所有这些升级选项确保升级后的数据库从全文性能增强功能中完全受益。  
  
## <a name="considerations-for-choosing-a-full-text-upgrade-option"></a>有关选择全文升级选项的注意事项  
 为升级选择升级选项时，请考虑以下几点：  
  
-   如何使用断字符？  
  
     [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中的全文搜索服务包括断字符和词干分析器。 这可能更改 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中特定文本模式或方案的全文查询结果。 因此，在选择适当的升级选项时，如何使用断字符非常重要：  
  
    -   如果使用的全文语言的断字符未发生更改，或者撤回准确性对您来说并不重要，则适合导入。 随后，如果遇到任何撤回问题，您只需通过重新生成全文目录即可升级到新的断字符。  
  
    -   如果您关心撤回准确性，并使用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]后已添加的断字符之一，则适合重新生成。  
  
-   是否基于整数全文键列生成了任何全文检索？  
  
     重新生成执行内部优化，在某些情况下该优化可提高升级的全文检索的查询性能。 具体来说，如果您具有的全文目录包含基表的全文键列为整数数据类型的全文检索，则重新生成将在升级后实现全文查询的理想性能。 在这种情况下，我们强烈建议使用 **“重新生成”** 选项。  
  
    > [!NOTE]  
    >  对于 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中的全文索引，建议采用整数数据类型作为全文键列。 有关详细信息，请参阅 [改进全文索引的性能](../../relational-databases/indexes/indexes.md)。  
  
-   使服务器实例处于联机状态的优先级是什么？  
  
     升级期间的导入或重新生成操作会占用很多 CPU 资源，这会延迟其余服务器实例的升级和联机。 如果使服务器实例尽快处于联机状态非常重要，并且希望在升级后运行手动填充，则适合 **“重置”** 。  
  
## <a name="additional-resources"></a>其他资源  
  