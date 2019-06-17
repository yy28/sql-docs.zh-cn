---
title: 定义时间智能计算使用商业智能向导 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2d3659fd80d09f5f0b5ec17301606b23810df3fe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63043065"
---
# <a name="define-time-intelligence-calculations-using-the-business-intelligence-wizard"></a>使用商业智能向导定义时间智能计算
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  时间智能增强功能是一项多维数据集增强功能，它可以将时间计算（或时间视图）添加到所选层次结构中。 此增强功能支持以下计算类别：  
  
-   到现在为止时间段。  
  
-   逐时间段增长。  
  
-   移动平均。  
  
-   并行时间段比较。  
  
 时间智能应用于有时间维度的多维数据集。 （时间维度是其 **Type** 属性设置为 **Time**的维度）。 另外，该维度的时间特性的 **Type** 属性还必须有适当的设置（如年份或月份）。 如果使用维度向导创建时间维度，将会正确设置维度及其特性的 **Type** 属性。  
  
 若要向多维数据集添加时间智能，请使用商业智能向导，并在 **“选择增强功能”** 页上选择 **“定义时间智能”** 选项。 然后此向导将指引您完成相应的步骤，以选择将向其添加时间智能的层次结构，并指定将对层次结构中的哪些成员应用时间智能。 在向导的最后一页，可以看到为了添加所选时间智能而要对 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库进行的更改。  
  
## <a name="selecting-a-time-hierarchy"></a>选择时间层次结构  
 在 **“选择目标层次结构和计算”** 页中，选择将应用时间增强功能的时间层次结构。 每次运行商业智能向导时，只能向一个时间层次结构应用时间增强功能。 如果希望向多个时间层次结构应用增强功能，请再次运行向导。  
  
 选择时间层次结构后，请在 **“可用时间计算”** 列表中选择将应用于该层次结构的计算。 列出的计算取决于在层次结构中的级别以及每个级别的特性的 **Type** 属性设置。 例如，“年份”层次结构支持“本年度截止到现在”和“年度同比增长量”，但是“季度”层次结构则不支持。  
  
> [!NOTE]  
>  Timeintelligence.xml 模板文件定义了在 **“可用时间计算”** 中列出的时间计算。 如果列出的计算不能满足需要，可以更改现有计算，或在 Timeintelligence.xml 文件中添加新的计算。  
  
> [!TIP]  
>  若要查看计算的说明，请使用向上和向下键突出显示该计算。  
  
## <a name="apply-time-views-to-members"></a>对成员应用时间视图  
 在 **“定义计算作用域”** 页中，可以指定要应用新时间视图的成员。 可以对下列对象之一应用新的时间视图：  
  
-   **帐户维度的成员** 在 **“定义计算作用域”** 页中， **“可用度量值”** 列表已包括帐户维度。 帐户维度的 **Type** 属性已设置为 **Accounts**。 如果有帐户维度但该维度没有出现在 **“可用度量值”** 列表中，则可以使用商业智能向导对该维度应用帐户智能。 有关详细信息，请参阅 [向维度中添加帐户智能](../../analysis-services/multidimensional-models/bi-wizard-add-account-intelligence-to-a-dimension.md)。  
  
-   **度量值** 可以不指定帐户维度，而指定应用时间视图的度量值。 在这种情况下，请选择要应用所选时间计算的视图。 例如，资产和负债是本年度截止到现在的数据；因此，不对资产或负债度量值应用“本年度截止到现在”的计算。  
  
## <a name="viewing-the-time-intelligence-enhancement"></a>查看时间智能增强功能  
 在商业智能向导的最后一页中，可以查看将对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库进行的更改。 对于时间智能增强功能，向导将按下表所述更改所选时间维度、关联的数据源视图以及关联的多维数据集。  
  
|Object|更改|  
|------------|------------|  
|时间维度|为每个计算（或视图）添加属性。|  
|数据源视图|在时间表中为时间维度中每个新属性添加计算列。|  
|多维数据集|添加计算成员，该成员定义了执行此计算的多维表达式 (MDX) 代码。|  
  
## <a name="see-also"></a>请参阅  
 [创建计算成员](../../analysis-services/multidimensional-models/create-calculated-members.md)  
  
  
