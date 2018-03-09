---
title: "了解增量生成 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- incremental generation [Analysis Services]
- Schema Generation Wizard, incremental generation
- relational schema [Analysis Services], incremental generation
ms.assetid: 3ca0aa63-3eb5-4fe9-934f-8e96dee84eaa
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8527382a85e1e85fb7981e69ea02304d2a7a940c
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
---
# <a name="understanding-incremental-generation"></a>了解增量生成
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
在生成初始架构后，可以使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]更改多维数据集定义和维度定义，然后返回架构生成向导。 向导会更新主题区域数据库和相关数据源视图中的架构以反映所做的更改，并且尽可能保留当前存在于要重新生成的表中的数据。 如果在初始生成之后更改表，则架构生成向导会使用下列规则在可能的情况下保留这些更改：  
  
-   如果表由向导在先前生成，则会被覆盖。 通过将数据源视图中表的 **AllowChangesDuringGeneration** 属性更改为 **false**，可以防止覆盖由向导生成的表。 如果可对表进行控制，则该表与任何其他用户定义表的处理方式相同，并且在重新生成过程中不受影响。 从生成中删除表之后，您可以稍后将数据源视图中表的 **AllowChangesDuringGeneration** 属性更改为 **true** ，并重新打开该表以便向导对其进行更改。 有关详细信息，请参阅[在数据源视图中更改属性 (Analysis Services)](../../analysis-services/multidimensional-models/change-properties-in-a-data-source-view-analysis-services.md)。  
  
-   如果表是通过向导以外的工具添加到数据源视图或基础数据库中，则不会被覆盖。  
  
 当架构生成向导重新生成先前在主题区域数据库中生成的表时，您可以选择让向导保留这些表中的现有数据。  
  
## <a name="supporting-data-preservation"></a>支持数据保留  
 作为通用规则，架构生成向导会保留存储在由其生成的表中的数据。 此外，如果将列添加到向导生成的表中，则向导也会保留这些数据。 您可以使用这项功能添加或修改维度和多维数据集，然后重新生成基础对象而不必重新加载存储在基础表中的数据。  
  
> [!NOTE]  
>  如果要加载分隔的文本文件中的数据，则还可以选择架构生成向导在重新生成过程中是否覆盖这些文件及其包含的数据。 文本文件既可以完全覆盖，也可以根本不覆盖。 架构生成向导不会部分覆盖这些文件。 默认情况下，这些文件不被覆盖。  
  
### <a name="partial-preservation"></a>部分保留  
 在某些情况下，架构生成向导不会保留现有的数据。 下表提供了一些示例，用于说明在哪些情况下，向导不会在重新生成过程中保留基础表中的所有现有数据。  
  
|数据类型更改|处理方式|  
|-------------------------|---------------|  
|不兼容的数据类型更改|架构生成向导会尽可能使用标准 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型转换，将现有数据从一种类型转换为另一种类型。 但是，当您将属性的数据类型更改为与现有数据不兼容的类型时，向导会删除受影响列的数据。|  
|引用完整性错误|如果在重新生成过程中更改包含数据的维度或多维数据集，并且更改导致引用完整性错误，则架构生成向导会删除外键表中的所有数据。 删除的数据并不限于导致违反外键约束的列或包含引用完整性错误的行。 例如，如果将维度键更改为具有非唯一数据或空数据的属性，则会删除外键表中的所有现有数据。 此外，删除某个表中的所有数据可能会产生级联影响，并可能会导致其他引用完整性被破坏。|  
|已删除的属性或维度|如果从维度中删除属性，则架构生成向导会删除映射到已删除属性的列。 如果删除维度，则向导会删除映射到已删除维度的表。 在这些情况下，向导会删除包含在已删除列或表中的数据。|  
  
 架构生成向导在删除任何数据之前会发出警告，以便您可以取消向导而不丢失任何数据。 但是，架构生成向导不能区别预料到的数据丢失和未预料到的数据丢失。 当您运行向导时，便会出现一个对话框，列出包含要删除的数据的表和列。 您既可以让向导继续运行并删除数据，也可以取消向导并修改对表和列所做的更改。  
  
## <a name="supporting-cube-and-dimension-changes"></a>支持多维数据集和维度更改  
 当您更改维度和多维数据集的属性时，架构生成向导会在基础主题区域数据库以及相关数据源视图中重新生成相应的对象，如下表中所述。  
  
 删除对象，如维度、多维数据集或属性。  
 架构生成向导会删除已删除对象映射到的基础对象。 如果将列添加到向导生成的表中，则新列并不会阻止该表被删除。 删除对象会导致存储在基础对象中的数据被删除，并且如果出现引用完整性错误，则还会导致其他数据被删除。  
  
 重命名对象，如维度、多维数据集或属性。  
 架构生成向导会重命名已重命名对象映射到的基础对象。 向导还会重命名所有受影响的对象，如主键。 存储在基础对象中的现有数据将被保留。  
  
 修改对象，如更改其数据类型。  
 架构生成向导会修改已更改对象映射到的基础对象。 除非新的数据类型与现有数据不兼容，否则将保留存储在数据库内基础对象中的现有数据。  
  
 添加新对象，如维度、多维数据集或属性。  
 架构生成向导会添加新对象映射到的基础对象。  
  
 如果架构生成向导因主题区域数据库中存在用户对象而无法进行所需的更改（因为数据库引擎返回错误），则架构生成向导会失败并显示由数据库引擎返回的错误。 例如，如果您在向导生成表后对该表创建主键约束或非聚集索引，则架构生成向导不会删除该表，因为向导并未创建约束或索引。  
  
## <a name="supporting-schema-changes"></a>支持架构更改  
 当您更改主题区域数据库或相关数据源视图中表或列的属性时，架构生成向导将按照下表所述处理更改。  
  
 删除由架构生成向导生成的表或列。  
 如果您删除由架构生成向导生成的表或列，则向导会重新生成已删除的表。 重新生成已删除的表或列时，向导不会发出警告。  
  
 更改由架构生成向导生成的表或列的属性。  
 如果修改由架构生成向导生成的表或列的属性，则该向导不会对表进行更改，而直接重新生成更改后的表。 例如，如果更改由架构生成向导生成的列的数据类型或为空性，或者更改该向导生成的表的文件组，则在重新生成后不会保留这些更改。 在不对对象进行更改，而直接重新生成更改后的对象时，向导不会发出警告。  
  
 将列添加到由架构生成向导生成的表中，或者将表添加到主题区域数据库或临时区域数据库中。  
 如果您将列添加到由架构生成向导生成的表中，则该向导会在重新生成过程保留附加的列以及该列中存储的所有数据。 但是，如果您将表添加到主题区域数据库或临时区域数据库中，则架构生成向导不会合并新表。 已添加的列或已添加的表不会在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库、DTS 包、数据源视图或者所生成架构中的任何其他位置上得以反映。  
  
## <a name="supporting-data-source-and-data-source-view-changes"></a>支持数据源和数据源视图更改  
 在重新运行架构生成向导时，它重用初始生成使用的相同数据源和数据源视图。 如果您添加数据源或数据源视图，则向导不会使用该数据源或数据源视图。 如果您在初始生成后删除原始数据源或数据源视图，则必须从头运行向导。 向导中的所有先前设置也会被删除。 下次运行架构生成向导时，基础数据库中任何绑定到已删除数据源或数据源视图的现有对象都被视为用户创建的对象。  
  
 如果数据源视图并未反映基础数据库生成时的实际状态，则架构生成向导在生成主题区域数据库架构或临时区域数据库架构时可能会遇到错误。 例如，如果数据源视图指定将列的数据类型设置为 **int**，但该列的数据类型实际设置为 **string**，则架构生成向导会将外键的数据类型设置为 **int** 以便与数据源视图相匹配，而在创建关系时会失败，因为实际的数据类型为 **string**。  
  
 另一方面，如果您将数据源连接字符串更改为先前生成的其他数据库，则不会生成任何错误。 将会使用新的数据库，并且不会对先前数据库进行任何更改。  
  
## <a name="see-also"></a>另请参阅  
 [管理对数据源视图和数据源更改](../../analysis-services/multidimensional-models/manage-changes-to-data-source-views-and-data-sources.md)   
 [架构生成向导 &#40;Analysis Services &#41;](../../analysis-services/multidimensional-models/schema-generation-wizard-analysis-services.md)  
  
  
