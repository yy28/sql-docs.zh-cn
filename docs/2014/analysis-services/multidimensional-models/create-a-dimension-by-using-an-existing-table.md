---
title: 使用现有表创建维度 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [Analysis Services], dimensions
- main dimension tables
- dimensions [Analysis Services], standard
- standard dimensions [Analysis Services]
ms.assetid: edd96fbe-1b1c-445a-95d6-7a025e0ee868
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5e65c2b8d543455a168bddc1be5ae5594c2ba8c3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66076423"
---
# <a name="create-a-dimension-by-using-an-existing-table"></a>使用现有表创建维度
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，您可以使用中[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的维度向导，通过现有表创建维度。 在维度向导的 **“选择创建方法”** 页上选择 **“使用现有表”** 选项可执行此操作。 选择此选项后，向导将基于现有数据源视图中的维度表、维度表中的列以及表中各列之间的任何关系构建维度结构。 该向导从源表和相关表中抽取样本数据。 此数据用于定义基于维度表中的列的属性列，以及定义属性的层次结构（称为“用户定义”** 的层次结构）。 使用维度向导创建维度后，可以使用维度设计器来添加、删除和配置维度中的属性和层次结构。  
  
 如果您要使用现有表来创建维度，则维度向导将指导您执行以下操作：  
  
-   指定源信息  
  
-   选择相关表  
  
-   选择维度属性  
  
-   定义帐户智能  
  
> [!NOTE]  
>  有关与本主题中信息对应的分步说明，请参阅 [使用维度向导创建维度](create-a-dimension-using-the-dimension-wizard.md)。  
  
## <a name="specifying-the-source-information"></a>指定源信息  
 可在 **“指定源信息”** 页上指定源信息。 首先应选择数据源视图，该数据源视图包含维度将基于的表。 然后为要定义的维度指定主维度表。 主维度表是直接链接到事实数据表的表。 例如，指定 Product 表作为“产品”维度的主表，或为“雇员”维度指定 Employee 表。 向导会自动选择基于数据源视图中主键的键列。 不过，您可以根据需要更改键列。 键列确定维度的成员。 例如，将 ProductKey 定义为“产品”维度的键列。  
  
 可以选择定义包含成员名称的列。 默认情况下，向用户显示的成员名称是来自键列的值。 键列中的值（例如 ProductID 或 EmployeeID）通常是系统生成的唯一键，对用户而言毫无意义。 如果您将向用户显示的名称更改为维度中其他列的相应值，则这通常可以向用户提供更有意义的信息。 例如，可以定义包含产品名称或雇员姓名的成员名称列。 如果更改成员名称，则用户将看到更具说明性的名称，但是查询仍将使用键列值，以正确区分使用相同名称的成员。 如果为键列指定组合键，还必须指定为键属性提供成员值的列。 有关如何配置特性属性的详细信息，请参阅 [维度特性属性参考](dimension-attribute-properties-reference.md)。  
  
## <a name="selecting-related-tables"></a>选择相关表  
  
> [!NOTE]  
>  如果主维度表与其他维度表之间没有在数据源视图中定义的任何关系，则向导将跳过此步骤。  
  
 若要生成雪花型维度，请在 **“选择相关表”** 页中指定从中定义其他属性的相关表。 例如，生成要在其中定义客户所在地域表的客户维度。 在这种情况下，可以将地域表定义为相关表。  
  
## <a name="selecting-dimension-attributes"></a>选择维度属性  
 选择维度表后，可以使用 **“选择维度属性”** 页来基于这些表选择要包含在维度中的属性。 所有这些表中的全部基础列都可用作潜在维度属性。 必须选择并启用维度键属性才能进行浏览。  
  
 默认情况下，向导将属性类型设置为 `Regular`。 不过，您可能希望将特定属性映射到另一种可更好地表达数据的属性类型。 例如， [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] DW 示例数据库中的 dbo.DimAccount 表包含提供帐号的 AccountCodeAlternateKey 列。 你可能希望将此属性`Regular`映射到`Account Number`类型，而不是将此属性的类型设置为。  
  
> [!NOTE]  
>  如果创建维度时没有设置维度类型和标准属性类型，则在创建维度后可使用商业智能向导设置这些值。 有关详细信息，请参阅 [向维度中添加维度智能](bi-wizard-add-dimension-intelligence-to-a-dimension.md) 或（对账户类型维度而言） [向维度中添加帐户智能](bi-wizard-add-account-intelligence-to-a-dimension.md)。  
  
 向导会基于指定的属性类型自动设置维度类型。 向导中指定的属性类型将设置特性的 `Type` 属性。 维度及其特性的 `Type` 属性设置可向服务器和客户端应用程序提供有关维度内容的信息。 在某些情况下，这些 `Type` 属性设置只为客户端应用程序提供指导信息，并且是可选的。 在其他情况下，例如“帐户”维度、“时间”维度或“货币”维度，这些 `Type` 属性设置确定基于服务器的特定行为，并且可能是实现某些多维数据集行为所必需的。  
  
 有关维度和属性类型的详细信息，请参阅 [维度类型](../multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)、 [配置属性类型](attribute-properties-configure-attribute-types.md)。  
  
## <a name="defining-account-intelligence"></a>定义帐户智能  
  
> [!NOTE]  
>  仅当在向导的“选择维度属性”**** 页上定义“帐户类型”**** 维度属性时，维度向导才显示此步骤。  
  
 使用 **“定义帐户智能”** 页可创建“帐户”类型的维度。 若要创建“帐户”类型的维度，必须将 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支持的标准帐户类型映射到维度中帐户类型属性的成员。 服务器使用这些映射为每种类型的帐户数据提供单独的聚合函数和别名。  
  
 向导提供了具有以下列的表来映射这些帐户类型：  
  
-   
  **“源表帐户类型”** 列，列出来自数据源表的帐户类型。  
  
-   “内置帐户类型”**** 列，列出服务器支持的相应标准帐户类型。 如果源数据使用标准名称，则向导会自动将源类型映射为服务器类型，然后使用此信息填充“内置帐户类型”**** 列。 如果服务器不映射帐户类型或您希望更改映射，可以从“内置帐户类型”**** 列的列表中选择其他类型。  
  
> [!NOTE]  
>  如果向导创建“帐户”维度时未映射帐户类型，则在创建维度后可使用商用智能向导配置这些映射。 有关详细信息，请参阅 [向维度中添加帐户智能](bi-wizard-add-account-intelligence-to-a-dimension.md)。  
  
## <a name="completing-the-wizard"></a>完成向导  
 向导扫描维度表以检测关系。 向导将在雪花型维度的键属性之间自动创建属性关系。  
  
 向导还会自动检测该维度中是否存在父子关系。 当父属性引用维度的键属性成员时，即存在父子关系。 此关系定义层次结构关系以及维度的叶成员之间的聚合路径。 有关父子层次结构的详细信息，请参阅 [父子层次结构中的属性](parent-child-dimension-attributes.md)。  
  
 在 **“完成向导”** 页中，输入新维度的名称并查看维度结构即完成该向导。  
  
## <a name="see-also"></a>另请参阅  
 [通过在数据源中生成非时间表来创建维度](create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md)   
 [通过生成时间表来创建时间维度](create-a-time-dimension-by-generating-a-time-table.md)   
 [维度特性属性参考](dimension-attribute-properties-reference.md)   
 [通过生成时间表来创建时间维度](create-a-time-dimension-by-generating-a-time-table.md)   
 [通过在数据源中生成非时间表来创建维度](create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md)  
  
  
