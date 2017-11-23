---
title: "维度和分区的配置字符串存储空间 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 987f6cfc-da82-4b2e-96ef-a8af88339e5f
caps.latest.revision: "21"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b16b14e2fb2fd703905245f9e779fd83b7f35cb4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="configure-string-storage-for-dimensions-and-partitions"></a>配置维度和分区的字符串存储
  可以重新配置字符串存储，以在维度属性或分区中容纳超过 4 GB 文件大小的字符串存储限制的极大字符串。 如果你的维度或分区包含此大小的字符串存储，则对于本地和链接（本地或远程）对象，你可以通过在维度或分区级别更改“StringStoresCompatibilityLevel”属性来解决文件大小限制。  
  
 请注意，你可以只在需要额外容量的对象上增加字符串存储空间。 在大多数的多维模型中，字符串数据与维度相关联。 但是，此设置对包含基于字符串的非重复计数度量值的分区也非常有用。 因为此设置针对字符串，所以数字数据不受影响。  
  
 此属性的有效值包括以下项：  
  
|“值”|Description|  
|-----------|-----------------|  
|**1050**|指定默认的字符串存储体系结构，即受到每个存储 4 GB 的最大文件大小的约束。|  
|**1100**|指定较大的字符串存储空间，支持每个存储区最多 40 亿个唯一字符串。|  
  
> [!IMPORTANT]  
>  更改某一对象的字符串存储设置要求您重新处理该对象本身以及任何依赖对象。 处理是完成这个过程所必需的。  
  
 本主题包含以下各节：  
  
-   [关于字符串存储](#bkmk_background)  
  
-   [先决条件](#bkmk_prereq)  
  
-   [步骤 1：在 SQL Server Data Tools 中设置 StringStoreCompatiblityLevel 属性](#bkmk_step1)  
  
-   [步骤 2：处理对象](#bkmk_step2)  
  
##  <a name="bkmk_background"></a> 关于字符串存储  
 字符串存储配置是可选的，这意味着即使是你创建的新数据库，也可以使用受到 4 GB 最大文件大小限制的默认字符串存储体系结构。 使用较大的字符串存储体系结构对性能的影响虽然很小，但也是较为明显的。 只有在您的字符串存储文件接近或达到 4 GB 的上限时，才应使用可缩放字符串存储体系结构。  
  
> [!NOTE]  
>  此设置不适用于数据挖掘模型。 当前，对于包含数据挖掘结构的模型，仍可能会遇到 GB 级的文件大小限制。  
  
 在 Analysis Services 多维数据库中，字符串与数值数据分别进行存储，以便允许基于数据特性进行优化。 字符串数据通常位于表示名称或说明的维度属性中。 在非重复计数度量值中也可能具有字符串数据。 字符串数据也可以用于键中。  
  
 您可以按其文件扩展名（例如 asstore、.bstore、.ksstore 或 .string 文件）标识字符串存储。 默认情况下，上述每种文件都具有 4 GB 的上限。 在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]中，您可以通过指定允许字符串存储按需增大的其他存储机制，取代这一最大文件大小。  
  
 与限制物理文件大小的默认字符串存储体系结构相反，较大的字符串存储空间基于字符串的最大数目。 较大的字符串存储空间的上限是 40 亿个唯一字符串或 40 亿条记录（以二者中最先达到限制条件的为准）。 较大的字符串存储空间创建同样大小的记录，每个记录等于 64K 页。 如果您具有在单个记录中放不下的非常长的字符串，则有效限制将小于 40 亿个字符串。  
  
##  <a name="bkmk_prereq"></a> 先决条件  
 你必须具有 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或更高版本的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。  
  
 维度和分区必须使用 MOLAP 存储。  
  
 数据库的兼容级别必须设置为 1100。 如果你使用 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 和 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或更高版本的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]创建了或部署了某一数据库，则该数据库的兼容级别已设置为 1100。 如果你将在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 早期版本中创建的数据库移动到 ssSQL11 或更高版本，则必须更新兼容级别。 对于要移动而不是重新部署的数据库，您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 来设置兼容级别。 有关详细信息，请参阅 [多维数据库的兼容级别 (Analysis Services)](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)。  
  
##  <a name="bkmk_step1"></a> 步骤 1：在 SQL Server Data Tools 中设置 StringStoreCompatiblityLevel 属性  
  
1.  使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]，打开包含要修改的维度或分区的项目。  
  
2.  若要更改维度的字符串存储，请打开解决方案资源管理器。 双击您要修改字符串存储的维度。  
  
3.  在维度设计器的“属性”窗格中，请确保选择该维度的父节点（例如，如果维度为 Customers，则选择 Customers，而不是其子属性之一）。  
  
4.  在“属性”窗格的“高级”部分中，将 **StringStoresCompatibilityLevel** 设置为 **1100**。 对于要求较大存储空间的其他维度重复上述设置，否则将其余维度的值保持为 **1050** 。  
  
5.  对于分区，请从解决方案资源管理器中打开一个多维数据集。  
  
6.  单击“分区”选项卡。  
  
7.  展开分区，选择需要额外存储容量的分区，然后修改 **StringStoresCompatibilityLevel** 属性。  
  
8.  保存该文件。  
  
##  <a name="bkmk_step2"></a> 步骤 2：处理对象  
 在您处理对象后，将使用新的存储体系结构。 处理对象也表明您已成功解决了存储约束问题，因为以前报告字符串存储溢出情况的错误不再出现了。  
  
-   在解决方案资源管理器中，右键单击刚修改的维度，然后选择“处理”。  
  
 您必须对使用新字符串存储体系结构的每个对象都使用“处理全部”选项。 在处理前，请确保对维度运行影响分析，以便检查依赖对象是否也要求重新处理。  
  
## <a name="see-also"></a>另请参阅  
 [用于处理的工具和方法 (Analysis Services)](../../analysis-services/multidimensional-models/tools-and-approaches-for-processing-analysis-services.md)   
 [处理选项和设置 (Analysis Services)](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)   
 [分区存储模式和处理](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md)   
 [维度存储](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-storage.md)  
  
  
