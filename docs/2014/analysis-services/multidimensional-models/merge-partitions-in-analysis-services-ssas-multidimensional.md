---
title: 在 Analysis Services 中合并分区（SSAS-多维） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- partitions [Analysis Services], merging
- merging partitions [Analysis Services]
ms.assetid: b3857b9b-de43-4911-989d-d14da0196f89
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 365f89286a59057efa39b503eedaedebb875c039
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66073652"
---
# <a name="merge-partitions-in-analysis-services-ssas---multidimensional"></a>在 Analysis Services 中合并分区（SSAS - 多维）
  您可以将现有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库中的分区进行合并，以整合来自相同度量值组的多个分区的事实数据。  
  
 [常见方案](#bkmk_Scenario)  
  
 [惠?](#bkmk_prereq)  
  
 [在合并分区后更新分区源](#bkmk_Where)  
  
 [按事实数据表或命名查询分段的分区的特殊注意事项](#bkmk_fact)  
  
 [如何使用 SSMS 合并分区](#bkmk_partitionSSMS)  
  
 [如何使用 XMLA 合并分区](#bkmk_partitionsXMLA)  
  
##  <a name="common-scenarios"></a><a name="bkmk_Scenario"></a>常见方案  
 分区应用的唯一最常见配置涉及到跨时间维度分离数据。 与每个分区关联的时间的粒度因特定于项目的业务需求而有所不同。 例如，可能用年数进行分段，而最近一年用月数除，并为活动月单独加上一个分区。 活动月分区定期取用新数据。  
  
 活动月份完成后，该分区被重新合并到截至到当前日期的分区中的月，该过程继续进行。 到年末时，就会形成一个完整的新的年分区。  
  
 正如这种情况所示，合并分区可能成为定期执行的一项例行任务，这可以为整合与组织历史数据提供一种渐进的方法。  
  
##  <a name="requirements"></a><a name="bkmk_prereq"></a> 要求  
 只有符合下列所有条件的分区才能合并：  
  
-   分区具有相同的度量值组。  
  
-   分区具有相同的结构。  
  
-   分区必须处于已处理状态。  
  
-   分区具有相同的存储模式。  
  
-   分区包含相同的聚合设计。  
  
-   分区共享相同的字符串存储兼容级别（仅适用于已分区的非重复计数度量值组）。  
  
 如果目标分区为空（即它具有聚合设计，但是没有聚合），则合并时将删除源分区的聚合。 您必须对分区运行“处理索引”、“处理全部”或“处理默认值”才能生成聚合。  
  
 远程分区只能与使用同一个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]远程实例定义的其他远程分区进行合并。  
  
> [!NOTE]  
>  如果您在结合使用本地和远程分区，则也可以创建包括组合数据的新分区，删除不再使用的分区。  
  
 若要创建一个准备在将来进行合并的分区，在分区向导中创建该分区时，您可以选择从另一个多维数据集分区复制聚合设计。 这将确保这些分区具有相同的聚合设计。 当这些分区进行合并时，源分区的聚合和目标分区的聚合将组合到一起。  
  
##  <a name="update-the-partition-source-after-merging-partitions"></a><a name="bkmk_Where"></a>合并分区后更新分区源  
 分区通过查询（如用于处理数据的 SQL 查询 WHERE 子句）或通过表或为分区提供数据的命名查询进行分段。 分区的 `Source` 属性指示分区是绑定到查询还是表。  
  
 当您合并分区时，将整合分区的内容，但是不会更新 `Source` 属性以反映分区的范围变大。 这就意味着，如果您以后重新处理一个保留初始 `Source` 的分区，则您将从该分区获得不正确的数据。 该分区将错误地在父项级别聚合数据。 下面的示例对这种行为进行了演示。  
  
 **问题**  
  
 假设您有一个多维数据集包含有关三种软饮料产品的信息。 该多维数据集有三个使用相同事实数据表的分区。 这些分区按产品进行分段。 第 1 分区包含有关 [ColaFull] 的数据，第 2 分区包含有关 [ColaDecaf] 的数据，第 3 分区包含有关 [ColaDiet] 的数据。 如果第 3 分区合并到第 2 分区中，则所得分区（第 2 分区）中的数据将是正确的，并且多维数据集的数据也将是准确的。 但是，当处理第 2 分区时，其内容可能由处于产品级别的成员的父级所决定。 此父级 [SoftDrinks] 还包含第 1 分区中的产品 [ColaFull]。 在处理第 2 分区时，将会加载所有软饮料的数据，包括 [ColaFull]。 于是多维数据集就包含了有关 [ColaFull] 的重复数据，并返回给最终用户不正确的数据。  
  
 **解决方案**  
  
 解决方案是通过调整 WHERE 子句或命名查询，或手动合并来自底层事实数据表的数据来更新 `Source` 属性，以确保以后的处理能考虑到分区的范围扩大而正确进行。  
  
 在此示例中，将第 3 分区合并到第 2 分区后，可以在所得的第 2 分区中提供一个筛选（例如 ("Product" = 'ColaDecaf' OR "Product" = 'ColaDiet')），用以指定：只从事实数据表中提取有关 [ColaDecaf] 和 [ColaDiet] 的数据，并排除有关 [ColaFull] 的数据。 作为替代方法，也可以在创建第 2 分区和第 3 分区时为它们指定筛选，而在合并进程中这些筛选将组合。 不论哪种情况，处理完分区之后，多维数据集都将不包含重复数据。  
  
 **结论**  
  
 合并分区后，请始终检查 `Source` 以验证筛选器适合于合并后的数据。 如果您从一个包含第一、二、三季度的历史数据的分区开始，现在要合并第四季度的数据，则必须调整筛选器，以包含第四季度数据。 否则，以后处理该分区时将导致错误的结果。 这对第四季度将是不正确的。  
  
##  <a name="special-considerations-for-partitions-segmented-by-fact-table-or-named-query"></a><a name="bkmk_fact"></a>按事实数据表或命名查询分段的分区的特殊注意事项  
 除了查询之外，分区也可以按表或命名查询分段。 如果源分区和目标分区使用同一数据源或数据源视图中的同一事实数据表，则在合并分区后 `Source` 属性有效。 它指定适合于所得分区的事实数据表数据。 因为所得分区所需的事实数据就在事实数据表中，所以无需对 `Source` 属性进行任何修改。  
  
 对于使用来自多个事实数据表或命名查询的数据的分区，需要执行其他工作。 您必须手动将来自源分区的事实数据表的事实数据合并到目标分区的事实数据表中。  
  
 或者，您还可以将合并后分区的源指定为一个返回两个不同的事实数据表的内容的命名查询。 如果不执行此手动步骤，事实数据表所包含的信息就不会完整。  
  
 同样，从命名查询获取分段数据的分区也需要更新。 合并后的分区现在必须具有返回之前从不同命名查询获得的合并结果集的命名查询。  
  
## <a name="partition-storage-considerations-molap"></a>分区存储注意事项：MOLAP  
 合并 MOLAP 分区时，存储在分区的多维结构中的事实数据也将合并。 这将生成一个内部完整而一致的分区。 然而，存储在 MOLAP 分区中的事实数据是事实数据表中事实数据的副本。 在随后处理分区时，系统将删除多维结构中的事实数据（仅适用于完全和刷新），而且将从由分区的数据源和筛选器所指定的事实数据表复制数据。 如果源分区所使用的事实数据表与目标分区所使用的不同，则必须手动合并源分区的事实数据表和目标分区的事实数据表，以确保对所得分区进行处理时能有一套完整的数据集。 如果两个分区基于不同的命名查询，则同样需要执行这一操作。  
  
> [!IMPORTANT]  
>  在经过处理之前，带有不完整事实数据表的已合并 MOLAP 分区包含事实数据表数据的一个内部合并副本，而且此分区可以正常运行。  
  
## <a name="partition-storage-considerations-holap-and-rolap-partitions"></a>分区存储注意事项：HOLAP 和 ROLAP 分区  
 合并具有不同事实数据表的 HOLAP 或 ROLAP 分区时，不会自动合并事实数据表。 除非手动合并事实数据表，否则只有与目标分区关联的事实数据表才可用于所得分区。 与源分区关联的事实数据无法用于在所得分区中深化数据，并且处理分区时聚合不会从不可用的表中汇总数据。  
  
> [!IMPORTANT]  
>  带有不完整事实数据表的已合并 HOLAP 或 ROLAP 分区包含精确的聚合，但包含的事实数据不完整。 引用缺少的事实数据的查询将返回错误数据。 处理该分区时，只通过可用的事实数据计算聚合。  
  
 除非用户试图深化到不可用的表中的事实数据，或执行一个要求从不可用的表中得到事实数据的查询，否则您可能不会注意到缺少某些表，不会注意到这些表还不可用。 因为聚合在合并进程中将组合，所以其结果只基于聚合的查询会返回准确数据，而其他查询则可能返回不准确的数据。 即使在所得分区的处理完成后，您可能也不会注意到不可用的事实数据表中缺少的数据（尤其是这些数据只代表组合数据的一小部分时）。  
  
 事实数据表的合并可在分区合并之前或之后进行。 但是，在这两项操作都完成之前，聚合不能准确地表示基础事实数据。 如果要对访问不同事实数据表的 HOLAP 或 ROLAP 分区进行合并，建议您在用户未连接到包含这些分区的多维数据集时进行。  
  
##  <a name="how-to-merge-partitions-using-ssms"></a><a name="bkmk_partitionSSMS"></a>如何使用 SSMS 合并分区  
  
> [!IMPORTANT]  
>  合并分区之前，首先复制数据筛选信息（通常是基于 SQL 查询进行筛选的 WHERE 子句）。 以后，合并完成后，您应该更新包含累积事实数据的分区的“分区源”属性。  
  
1.  在对象资源管理器中，展开包含要合并分区的多维数据集的“度量值组”**** 节点，展开“分区”****，右键单击要被合并或要合并到的分区。 例如，如果您要将每个季度的事实数据移到存储年度事实数据的分区，请选择包含年度事实数据的分区。  
  
2.  单击 "**合并分区**" 打开 "**合并\<分区分区名称>** " 对话框。  
  
3.  在 **“源分区”** 下，选中要与目标分区合并的每个源分区旁边的复选框，然后单击 **“确定”**。  
  
    > [!NOTE]  
    >  源分区合并到目标分区后，将立即删除源分区。 合并完成后，刷新“分区”文件夹以更新其内容。  
  
4.  右键单击包含累积数据的分区，然后选择“属性”****。  
  
5.  打开`Source`属性，并修改 WHERE 子句，使之包括您刚合并的分区数据。 请记住， `Source`属性不会自动更新。 如果在不首先更新的`Source`情况下重新处理，则可能不会获得所有预期的数据。  
  
##  <a name="how-to-merge-partitions-using-xmla"></a><a name="bkmk_partitionsXMLA"></a> 如何使用 XMLA 合并分区  
 有关信息，请参阅此主题[合并分区 (XMLA)](../multidimensional-models-scripting-language-assl-xmla/merging-partitions-xmla.md)。  
  
## <a name="see-also"></a>另请参阅  
 [处理 Analysis Services 对象](processing-analysis-services-objects.md)   
 [Analysis Services 多维数据 &#40;分区&#41;](../multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [创建和管理本地分区 &#40;Analysis Services&#41;](create-and-manage-a-local-partition-analysis-services.md)   
 [创建和管理远程分区 &#40;Analysis Services&#41;](create-and-manage-a-remote-partition-analysis-services.md)   
 [设置分区写回](set-partition-writeback.md)   
 [启用写入的分区](../multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions.md)   
 [配置维度和分区的字符串存储](configure-string-storage-for-dimensions-and-partitions.md)  
  
  
