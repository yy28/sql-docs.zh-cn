---
title: 维度启用写功能 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3d6acb9fa8d9f268130e0c417507a4200c022b27
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="write-enabled-dimensions"></a>启用写操作的维度
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  
  
 维度中的数据通常为只读数据。 但在某些情况下，可能需要为维度启用写操作。 在[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，写入启用维度使业务用户能够修改维度的内容并查看更改的即时影响维度的层次结构上。 基于单个表的任何维度均可启用写操作。 在启用写操作的维度中，业务用户和管理员都可以更改、移动、添加和删除维度中的属性成员。 这些更新统称为*维度写回*。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支持对所有维度属性的维度写回，维度的任何成员均可修改。 对于启用写操作的多维数据集或分区，更新存储在独立于多维数据集的源表的写回表中。 不过，对于启用写操作的维度，更新直接记录在维度的表中。 同样，如果启用写操作的维度包括在具有多个分区的多维数据集中（其中，某些数据源或所有数据源具有维度表的副本），则在写回过程中只更新原始维度表。  
  
 启用写操作的维度和启用写操作的多维数据集拥有互不相同而又相互补充的功能。 启用写操作的维度使业务用户可以更新成员，而启用写操作的多维数据集则使业务用户可以更新单元值。 虽然这两个功能是互补的，但您不必同时使用它们。 维度不必包括在多维数据集中即可进行维度写回。 启用写操作的维度也可以包括在没有启用写操作的多维数据集中。 可使用不同的过程对维度和多维数据集启用写操作和维护它们的安全性。  
  
 对维度写回具有下列限制：  
  
-   创建新成员时，必须包括维度中的所有属性。 您不能插入未指定维度的键属性值的成员。 因此，创建成员时，应服从对维度表定义的任何约束（例如，非空键值）。  
  
-   只对星型架构支持维度写回。 也就是说，维度必须基于与事实数据表直接相关的单个维度表。 对维度启用写操作后，当您部署到现有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库或生成 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目时，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将验证此要求。  
  
 可以修改或删除写回维度的任何现有成员。 删除成员时，删除操作将级联到所有子成员。 例如，在包含“国家（地区）”、“省市自治区”、“市县”和“客户”属性的“客户”维度中，删除某一国家（地区）时，将同时删除隶属该国家（地区）的所有省市自治区、市县和客户。 如果某一国家（地区）只有一个省市自治区，则删除省市自治区时也会删除该国家（地区）。  
  
 写回维度的成员只能在同一个级别内移动。 例如，市县可以移到另一个国家（地区）或省市自治区的“市县”级别，但市县不能移到“省市自治区”或“国家（地区）”级别。 父-子层次结构中所有成员都是叶成员，因此成员可能被移动到任何级别以外**（全部）**级别。  
  
 如果删除父子层次结构的某个成员，则该成员的子级便会移到其父级。 对于关系表中删除的成员，需要具有更新权限，但是对于移动的成员则不需要任何权限。 当应用程序移动父子层次结构中的某一成员时，其可在 UPDATE 操作中指定该成员的后代是一起移动，还是移到该成员的父级。 若要以递归方式删除父子层次结构中的成员，则用户必须对关系表中该成员及其所有后代具有更新权限。  
  
> [!NOTE]  
>  对父子层次结构中的父特性的更新一定不能包括对任何其他属性或特性的更新。  
  
 对维度进行的所有更改将会修改维度结构。 对维度的每个更改被视为单个事务，需要增量处理来更新维度结构。 启用写操作的维度具有与任何其他维度相同的处理要求。  
  
> [!NOTE]  
>  链接维度不支持维度写回。  
  
## <a name="security"></a>Security  
 只有那些在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库角色中被授予对维度的读/写权限的业务用户，才可以更新启用写操作的维度。 对于每个角色，均可控制哪些成员可以更新，哪些成员不能更新。 要使业务用户能更新启用写操作的维度，其客户端应用程序必须支持此功能。 对于这些用户，启用写操作的维度必须包括在自上次更改维度以来处理过的多维数据集中。 有关详细信息，请参阅[授予对对象和操作的访问权限 (Analysis Services)](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)。  
  
 包括在“管理员”角色中的用户和组可更新启用写操作的维度的属性成员，即使维度不包括在多维数据集中也是如此。  
  
## <a name="see-also"></a>另请参阅  
 [数据库维度属性](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/database-dimension-properties.md)   
 [写入的分区](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions.md)   
 [维度 & #40;Analysis Services-多维数据 & #41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
