---
title: 通过生成时间表来创建时间维度 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2c5526075c563bfea107592c6e0d583feff3fde2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="create-a-time-dimension-by-generating-a-time-table"></a>通过生成时间表来创建时间维度
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，当源数据库中没有可用的时间表时，可以使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的维度向导创建时间维度。 在 **“选择创建方法”** 页上选择下列选项之一可执行此操作。  
  
-   **在数据源中生成时间表** 如果您具有在基础数据源中创建对象的权限，可选择此选项。 该向导将生成一个时间表并将此表存储在数据源中。 然后，该向导根据此时间表创建时间维度。  
  
-   **在服务器上生成时间表** 如果您没有在基础数据源中创建对象的权限，则选择此选项。 该向导将生成一个时间表并将此表存储在服务器上而不是数据源中。 （根据服务器上的时间表创建的维度称为“服务器时间维度”。）然后，该向导根据此表创建服务器时间维度。  
  
 创建时间维度时，需要指定时间段以及维度的开始日期和结束日期。 向导将使用指定的时间段创建时间属性。 处理维度时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会生成并存储支持指定日期和时间段所需的数据。 向导使用为时间维度创建的属性来建议维度的层次结构。 层次结构反映了不同时间段之间的关系，并且考虑了不同的日历。 例如，在标准日历层次结构中，“周”级别在“年”级别下显示，而不是在“月”级别下显示，因为各个年份中包含的周数非常平均，而各个月中包含的周数并不平均。 相反，在生产日历或报表日历层次结构中，各个月中包含的周数非常平均，因此“周”级别在“月”级别下显示。  
  
## <a name="define-time-periods"></a>定义时间段  
 使用向导的 **“定义时间段”** 页来指定要包含在维度中的日期范围。 例如，您可以选择一个从数据中最早年份的 1 月 1 日开始，并在当前年份过后的一或两年结束（允许执行更多事务）的范围。 不在该范围内的事务或者不显示，或者显示为维度中的未知成员，具体取决于该维度的 **UnknownMemberVisible** 属性设置。 您也可以更改数据所使用的周的第一天（默认值为星期日）。  
  
 选择在向导创建应用于您的数据的层次结构时要使用的时间段，如“年”、“半年”、“季度”、“四个月”、“月”、“十天”、“周”或“日期”。 您始终必须至少选择“日期”时间段。 “日期”属性是维度的键属性，因此，没有该属性，维度不能发挥作用。  
  
 在 **“时间成员名称所用的语言”**旁边，选择要用于标记维度成员的语言。  
  
 创建完基于日期范围的时间维度之后，您可以使用维度设计器添加或删除时间属性。 由于“日期”属性是维度的键属性，因此，不能将该属性从维度中删除。 若要对用户隐藏“日期”特性，可以将该特性的 **AttributeHierarchyVisible** 属性更改为 **False**。  
  
## <a name="select-calendars"></a>选择日历  
 当您创建时间维度时，所用日历始终包括标准（公历） 12 个月日历（从 1 月 1 日开始，到 12 月 31 日结束）。 在向导的 **“选择日历”** 页中，您可以指定维度中的层次结构所基于的其他日历。 有关日历类型的说明，请参阅 [创建日期类型维度](../../analysis-services/multidimensional-models/database-dimensions-create-a-date-type-dimension.md)。  
  
 根据您在向导的 **“定义时间段”** 页中选定的时间段的不同，日历选择确定在维度中创建的属性。 例如，如果你在向导的“定义时间段”页中选择“年”和“季度”时间段，在“选择日历”页中选择“会计日历”，则会为该会计日历创建 FiscalYear、FiscalQuarter 以及 FiscalQuarterOfYear 属性。  
  
 向导还会创建日历特定的层次结构，其中包含为该日历创建的属性。 对于每个日历，每个层次结构中的每个级别都汇总到其上面的级别中。 例如，在标准 12 个月日历中，向导创建“年 - 周”层次结构或“年 - 月”层次结构。 但是在标准日历中，各个月中包含的周数并不平均，因此，没有“年 - 月 - 周”这类层次结构。 相反，报表日历或生产日历中的各个月中包含的周数非常平均，因此在这些日历中，周级别汇总到月级别中。  
  
## <a name="completing-the-dimension-wizard"></a>完成维度向导  
 在 **“完成向导”** 页中，查看由向导创建的属性和层次结构，然后命名时间维度。 单击 **“完成”** 完成向导并创建维度。 创建维度完成后，可以使用维度设计器来更改维度。  
  
## <a name="see-also"></a>另请参阅  
 [多维模型中的数据源视图](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [创建日期类型维度](../../analysis-services/multidimensional-models/database-dimensions-create-a-date-type-dimension.md)   
 [数据库维度属性](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/database-dimension-properties.md)   
 [维度关系](../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [通过在数据源中生成非时间表来创建维度](../../analysis-services/multidimensional-models/create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md)  
  
  
