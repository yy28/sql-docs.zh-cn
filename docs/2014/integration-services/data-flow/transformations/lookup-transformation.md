---
title: 查找转换 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptrans.f1
helpviewer_keywords:
- Lookup transformation
- joining columns [Integration Services]
- cache [Integration Services]
- match exactly [Integration Services]
- lookups [Integration Services]
- exact matches [Integration Services]
ms.assetid: de1cc8de-e7af-4727-b5a5-a1f0a739aa09
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 69ed33b3967b3c807b21df0ab8a3a4a1cd07bebc
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939475"
---
# <a name="lookup-transformation"></a>查找转换
  查找转换通过联接输入列中的数据和引用数据集中的列来执行查找。 可以使用该查找在基于通用列的值的相关表中访问其他信息。  
  
 引用数据集可以是缓存文件、现有的表或视图、新表或 SQL 查询的结果。 查找转换使用 OLE DB 连接管理器或缓存连接管理器来连接到引用数据集。 有关详细信息，请参阅 [OLE DB 连接管理器](../../connection-manager/ole-db-connection-manager.md) 和 [缓存连接管理器](../../connection-manager/cache-connection-manager.md)。  
  
 可以用以下方式来配置查找转换：  
  
-   选择要使用的连接管理器。 如果要连接到数据库，请选择 OLE DB 连接管理器。 如果要连接到缓存文件，请选择缓存连接管理器。  
  
-   指定包含引用数据集的表或视图。  
  
-   通过指定 SQL 语句来生成引用数据集。  
  
-   指定输入和引用数据集间的联接。  
  
-   将引用数据集的列添加到查找转换输出中。  
  
-   配置缓存选项。  
  
 查找转换支持适用于 OLE DB 连接管理器的以下数据库访问接口：  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
-   Oracle  
  
-   DB2  
  
 查找转换试图在转换输入的值和引用数据集的值之间执行同等联接。 （同等联接意味着转换输入中的每一行都至少要与引用数据集中的一行匹配。）如果无法实现同等联接，则查找转换会执行下列操作之一：  
  
-   如果引用数据集中没有匹配项，则不会发生联接。 默认情况下，查找转换将没有匹配项的行视为错误。 但是，您可以将查找转换配置为将这些行重定向到无匹配输出。 有关详细信息，请参阅[查找转换编辑器（“常规”页）](../../lookup-transformation-editor-general-page.md)和[查找转换编辑器（“错误输出”页）](../../lookup-transformation-editor-error-output-page.md)。  
  
-   如果引用表中有多个匹配项，则查找转换只返回查找查询返回的第一个匹配项。 如果发现多个匹配项，则仅当转换被配置为将所有引用数据集加载到缓存中时查找转换才生成错误或警告。 在这种情况下，如果查找转换在填充缓存时检测到多个匹配项，则该查找转换将生成警告。  
  
 联接可以是组合联接，即可以将转换输入中的多个列联接到引用数据集中的列。 除了 DT_R4、DT_R8、DT_TEXT、DT_NTEXT 或 DT_IMAGE 外，转换支持联接其他任何数据类型的列。 有关详细信息，请参阅[Integration Services 数据类型](../integration-services-data-types.md)。  
  
 通常，将来自引用数据集的值添加到转换输出中。 例如，查找转换可以使用输入列的值从表中提取产品名，然后将产品名添加到转换输出中。 来自引用表的值可以替换列值，也可以添加到新列中。  
  
 查找转换执行的查找区分大小写。 因此，为了避免因数据中大小写不同而导致查找失败，首先请使用字符映射转换将数据转换为大写或小写。 然后在生成引用表的 SQL 语句中包含 UPPER 或 LOWER 函数。 有关详细信息，请参阅[字符映射表转换](character-map-transformation.md)、[UPPER (Transact-SQL)](/sql/t-sql/functions/upper-transact-sql) 和 [LOWER (Transact-SQL)](/sql/t-sql/functions/lower-transact-sql)。  
  
 查找转换具有以下输入和输出：  
  
-   输入。  
  
-   匹配输出。 匹配输出处理转换输入中那些在引用数据集内至少有一个匹配项的行。  
  
-   无匹配输出。 无匹配输出处理输入中在引用数据集内没有任何匹配项的行。 如果将查找转换配置为将无匹配项的行视为错误，则这些行会重定向到错误输出。 否则，转换会将这些行重定向到无匹配输出。  
  
    > [!NOTE]  
    >  在 [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)] 中，查找转换只有一个输出。 有关如何运行在中创建的查找转换的详细信息 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ，请参阅[升级查找转换](../../../sql-server/install/upgrade-lookup-transformations.md)。  
  
-   错误输出。  
  
## <a name="caching-the-reference-dataset"></a>缓存引用数据集  
 内存缓存存储引用数据集以及为数据创建索引的哈希表。 缓存保留在内存中，直到包执行完成。 您可以将缓存保留到缓存文件中 (.caw)。  
  
 将缓存保留到文件中时，系统加载缓存的速度会更快。 这可以提高查找转换和包的性能。 请注意，使用缓存文件时，您使用的数据不如数据库中的数据新。  
  
 下面是将缓存保留到文件中的其他好处：  
  
-   ***在多个包之间共享缓存文件。有关详细信息，请参阅***  [在完全缓存模式下使用缓存连接管理器实现查找转换](../../connection-manager/lookup-transformation-full-cache-mode-cache-connection-manager.md)  ***。***  
  
-   使用包部署缓存文件。 ***随后即可在多台计算机上使用该数据。*** 有关详细信息，请参阅 [为查找转换创建和部署缓存](create-and-deploy-a-cache-for-the-lookup-transformation.md)。  
  
-   使用原始文件源从缓存文件中读取数据。 随后即可使用其他数据流组件来转换或移动数据。 有关详细信息，请参阅 [Raw File Source](../raw-file-source.md)。  
  
    > [!NOTE]  
    >  缓存连接管理器不支持使用原始文件目标创建或修改的缓存文件。  
  
-   通过使用文件系统任务对缓存文件执行操作和设置属性。 有关详细信息，请参阅 [File System Task](../../control-flow/file-system-task.md)。  
  
 下面列出了各种缓存选项：  
  
-   在查找转换运行之前，通过使用表、视图或 SQL 查询生成引用数据集并将该引用数据集加载到缓存中。 您可以使用 OLE DB 连接管理器访问该数据集。  
  
     此缓存选项与 [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)]中查找转换的完全缓存选项兼容。  
  
-   在查找转换运行之前，从数据流中的已连接数据源或从缓存文件生成引用数据集并将该引用数据集加载到缓存中。 您可以使用缓存连接管理器并根据需要使用缓存转换来访问该数据集。 有关详细信息，请参阅 [缓存连接管理器](../../connection-manager/cache-connection-manager.md) 和 [缓存转换](cache-transform.md)。  
  
-   在执行查找转换过程中，通过使用表、视图或 SQL 查询生成引用数据集。 在引用数据集中有匹配项的行以及在该数据集中没有匹配项的行都会加载到缓存中。  
  
     超出缓存的内存大小后，查找转换会自动从缓存中删除最不常使用的行。  
  
     此缓存选项与适用于 [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)]中的查找转换的部分缓存选项兼容。  
  
-   在执行查找转换过程中，通过使用表、视图或 SQL 查询生成引用数据集。 没有缓存数据。  
  
     此缓存选项与 [!INCLUDE[ssISversion2005](../../../includes/ssisversion2005-md.md)]中查找转换的无缓存选项兼容。  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 在比较字符串时所用的方式不同。 如果查找转换配置为在查找转换运行之前将引用数据集加载到缓存中，则 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 将在缓存中执行查找比较。 否则，查找操作将使用参数化 SQL 语句并且 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 将执行查找比较。 这意味着，根据缓存类型的不同，查找转换可能会从同一查找表中返回不同数量的匹配项。  
  
## <a name="related-tasks"></a>Related Tasks  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。 有关详细信息，请参阅以下主题：  
  
-   [在不缓存模式或部分缓存模式下实现查找](implement-a-lookup-in-no-cache-or-partial-cache-mode.md)  
  
-   [在完全缓存模式下使用缓存连接管理器实现查找转换](../../connection-manager/lookup-transformation-full-cache-mode-cache-connection-manager.md)  
  
-   [在完全缓存模式下使用 OLE DB 连接管理器来实现查找转换](../../connection-manager/lookup-transformation-full-cache-mode-ole-db-connection-manager.md)  
  
-   [设置数据流组件的属性](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>相关内容  
  
-   msdn.microsoft.com 上的视频 [How to: Implement a Lookup Transformation in Full Cache Mode](https://go.microsoft.com/fwlink/?LinkId=131031)（如何在完全缓存模式下实现查找转换）  
  
-   blogs.msdn.com 上的博客项 [Best Practices for Using the Lookup Transformation Cache Modes](https://go.microsoft.com/fwlink/?LinkId=146623)（使用查找转换缓存模式的最佳实践）  
  
-   blogs.msdn.com 上的博客项 [Lookup Pattern: Case Insensitive](https://go.microsoft.com/fwlink/?LinkId=157782)（查找模式：不区分大小写）  
  
-   msftisprodsamples.codeplex.com 上的示例 [Lookup Transformation](https://go.microsoft.com/fwlink/?LinkId=267528)（查找转换）  
  
     有关安装 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 产品示例和示例数据库的信息，请参阅 [SQL Server Integration Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=267527)（SQL Server Integration Services 产品示例）。  
  
## <a name="see-also"></a>另请参阅  
 [模糊查找转换](fuzzy-lookup-transformation.md)   
 [字词查找转换](term-lookup-transformation.md)   
 [数据流](../data-flow.md)   
 [Integration Services 转换](integration-services-transformations.md)  
  
  
