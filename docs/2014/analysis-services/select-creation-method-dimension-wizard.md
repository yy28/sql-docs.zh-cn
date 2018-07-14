---
title: 选择创建方法 （维度向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.dimensiondefinition.f1
ms.assetid: 291b0b2d-a03a-4df6-82f7-90ad92d4d1cf
caps.latest.revision: 28
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9d10005b2b689078eb7677547ebfc905fbdcc996
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37267153"
---
# <a name="select-creation-method-dimension-wizard"></a>选择创建方法（维度向导）
  可以使用 **“选择创建方法”** 页选择如何创建维度。  
  
 **若要打开维度向导**  
  
-   在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 的**解决方案资源管理器**中，右键单击 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目的“维度”文件夹，然后单击“新建维度”。  
  
## <a name="options"></a>“常规”  
 **使用现有表**  
 从数据源中的一个或多个表创建维度。 可用于该维度的属性取决于表中数据的结构。  
  
 有关详细信息，请参阅 [使用现有表创建维度](multidimensional-models/create-a-dimension-by-using-an-existing-table.md)。  
  
 **数据源中生成时间表**  
 在基础数据源中创建时间表，然后使用该表创建时间维度。 不存在这类表，并且不想使用脚本创建表时，可使用此选项。 新的时间表将包含日期范围数据、属性和在向导中指定的日历。  
  
> [!NOTE]  
>  若要使用此选项，则您必须拥有在基础数据源中创建对象的权限。 如果没有在数据源中创建对象的权限，可以尝试改用 **“在服务器上生成时间表”** 选项。  
  
 有关详细信息，请参阅 [通过生成时间表来创建时间维度](multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md)。  
  
 **生成服务器上的时间表**  
 在服务器上直接创建时间表，然后使用该表创建时间维度。 如果没有在基础源数据中创建对象的权限，可以使用此选项。 新的时间维度将包含日期范围数据、属性和在向导中指定的日历。  
  
 有关详细信息，请参阅 [通过生成时间表来创建时间维度](multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md)。  
  
 **数据源中生成非时间表**  
 在没有基础关系数据源的情况下设计维度，然后为数据源生成必要的架构。 这种方法称为自上而下的建模。  
  
> [!NOTE]  
>  若要使用此选项，则您必须拥有在基础数据源中创建对象的权限。  
  
 生成维度可以使用模板，也可以不使用模板。 若要使用模板生成维度，请从 **“模板”** 列表中选择模板。  
  
 有关详细信息，请参阅 [通过在数据源中生成非时间表来创建维度](multidimensional-models/create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md)。  
  
 **模板**  
 选择要用于创建维度的模板。 模板提供面向特定商业用途的一组完整的属性和层次结构定义。  
  
> [!NOTE]  
>  仅当选择了“在数据源中生成非时间表”选项时，此选项才可用。  
  
## <a name="see-also"></a>请参阅  
 [维度向导的 F1 帮助](dimension-wizard-f1-help.md)   
 [维度&#40;Analysis Services-多维数据&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [多维模型中的维度](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
