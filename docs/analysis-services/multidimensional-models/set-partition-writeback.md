---
title: 设置分区写回 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 844aad81d49f16718cb795f443c3d8101e2ff771
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63020095"
---
# <a name="set-partition-writeback"></a>设置分区写回
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  如果对度量值组执行写启用操作，则最终用户可在浏览多维数据集数据时对其进行更改，所做的更改保存在一个称为“写回表”的单独表中，而不是多维数据集数据或源数据中。 浏览已启用写操作的分区的最终用户将看到对该分区在这个写回表中所做的全部更改的实际结果。  
  
 可以浏览或删除写回数据。 还可以将写回数据转换为分区。 在已启用写操作的分区上，可使用多维数据集角色授予用户和用户组读/写权限，并限制对分区中特定单元或单元组的访问。  
  
 有关写回的一个简短视频简介，请参阅 [向 Analysis Services 的 Excel 2010 写回](http://go.microsoft.com/fwlink/p/?LinkId=394951)。 关于此功能的更详细探讨，请参阅博客文章系列 [使用 Analysis Services 生成写回应用程序（博客）](http://go.microsoft.com/fwlink/?LinkId=394977)。  
  
> [!NOTE]  
>  仅对 SQL Server 关系数据库和数据市场支持写回，并且写回仅适用于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 多维模型。  
  
## <a name="how-to-write-enable-a-partition"></a>如何对分区执行写启用  
 通过在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的多维数据集设计器中对分区本身执行写启用操作，可以对分区的度量值组执行写启用。  
  
-   在多维数据集设计器中的“分区”选项卡上，右键单击一个分区，然后选择“写回设置”。   
  
-   在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，展开“数据库”|“多维数据集”|“度量值组”，然后右键单击“写回”并选择“启用写回”。    
  
 只有使用 SUM 聚合的度量值才支持写回。 在 AdventureWorks 示例数据库中，可以使用 Sales Targets 度量值组测试写回行为。  
  
 启用分区的写功能时，请指定用于存储写回表的表名称和数据源。 度量值组的任何后续更改都将记录在此表中。  
  
## <a name="browse-writeback-data-in-a-partition"></a>浏览分区中的写回数据  
 可以在“浏览数据”对话框中浏览多维数据集的写回表的内容，在多维数据集设计器的“分区”选项卡上右键单击启用了写操作的分区即可访问该对话框。    
  
## <a name="delete-writeback-data-or-disable-writeback"></a>删除写回数据或禁用写回  
 删除写回数据将清除写回缓存；在删除数据后，其他写回工作将立即在干净状态下执行。 禁用某个多维数据集分区的写回仅仅是关闭该分区的写回。  
  
## <a name="convert-writeback-data-to-a-partition"></a>将写回数据转换到分区  
 可以将分区写回表中的数据转换为分区。 此过程使得写回表成为新分区的事实数据表。  
  
> [!CAUTION]  
>  不正确地使用分区可导致多维数据集数据不准确。 有关详细信息，请参阅 [创建和管理本地分区 (Analysis Services)](../../analysis-services/multidimensional-models/create-and-manage-a-local-partition-analysis-services.md)。  
  
 将写回数据表转换为分区还会对分区禁用写功能。 分区单元的所有无限制读/写策略和读/写权限都将禁用，而且最终用户将无法更改显示的多维数据集数据。 （被禁用无限制读/写策略或读/写权限的最终用户仍然能够浏览多维数据集。）读取权限和有条件读取权限不受影响。  
  
 若要将写回数据转换为分区，请使用“转换到分区”对话框，可以通过右键单击 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中可写入的分区的写回表来访问该对话框。  您将指定分区的名称，并指定是在以后为分区设计聚合，还是在创建分区时为其设计聚合。 若要在选择分区时创建聚合，则必须选择复制现有分区中的聚合设计。 这通常（但不必须）是当前的写回分区。 还可以选择在创建分区时对其进行处理。  
  
## <a name="see-also"></a>请参阅  
 [可写入的分区](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions.md)   
 [在 Excel 2010 中启用以单元级别写回到 OLAP 多维数据集](http://go.microsoft.com/fwlink/p/?LinkId=394952)   
 [启用 Analysis Services 写回并使用它保护数据项](http://go.microsoft.com/fwlink/p/?LinkId=394953)  
  
  
