---
title: "创建 KPI 语句 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE KPI
- KPI
- CREATE_KPI
- CREATE
helpviewer_keywords:
- CREATE KPI statement
- key performance indicators [MDX]
ms.assetid: 87618fef-95e5-4dd0-a650-aeb60ccbddcb
caps.latest.revision: "18"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 9e153bf489ab3d06eb55c4226677c4913498b9f7
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="mdx-data-definition---create-kpi"></a>MDX 数据定义-创建 KPI
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  创建关键绩效指标 (KPI)。 KPI 是与多维数据集中的某个度量值组关联并用于评估业务或方案成败的计算集合。  
  
## <a name="syntax"></a>语法  
  
```  
  
CREATE KPI CURRENTCUBE | <Cube Name>.KPI_Name AS KPI_Value  
   [,Property_Name = Property_Value, ...n]  
```  
  
## <a name="arguments"></a>参数  
 *KPI_Name*  
 提供 KPI 名称的有效字符串。  
  
 *KPI_Value*  
 返回数值的有效多维表达式 (MDX) 表达式。  
  
 *Property_Name*  
 提供 KPI 属性名称的有效字符串。  
  
 *Property_Value*  
 定义 KPI 属性值的有效标量表达式。  
  
## <a name="remarks"></a>注释  
 指定当前连接的多维数据集以外的多维数据集将导致错误。 因此，应使用 CURRENTCUBE 来代替多维数据集名称，以表示当前的多维数据集。  
  
## <a name="kpi-properties"></a>KPI 属性  
 下表列出了所有的 KPI 属性。 这些属性都没有默认值。 因此，在为 KPI 属性指定某个特定值之前，针对该属性的查询会返回空值。  
  
|属性标识符|含义|  
|-------------------------|-------------|  
|GOAL|返回数值的有效 MDX 表达式。|  
|STATUS|返回数值的有效 MDX 表达式。|  
|STATUS_GRAPHIC|用于定义一组图形图像的字符串，这些图形图像将由客户端应用程序使用。|  
|TREND|返回数值的有效 MDX 表达式。|  
|TREND_GRAPHIC|用于定义一组图形图像的字符串，这些图形图像将由客户端应用程序使用。|  
|WEIGHT|返回数值的有效 MDX 表达式。|  
|CURRENT_TIME_MEMBER|返回时间维度成员的有效 MDX 表达式。 CURRENT_TIME_MEMBER 设置所有相对时间函数的参考点|  
|PARENT_KPI|指定父级 KPI 名称的字符串。|  
|CAPTION|客户端应用程序用作 KPI 标题的字符串。|  
|DISPLAY_FOLDER|指定显示文件夹的路径的字符串，客户端应用程序将在此处显示 KPI。 文件夹级别的分隔符由客户端应用程序定义。 有关工具和客户端提供[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，反斜杠 (\\) 是级别的分隔符。 若要为已定义的成员提供多个显示文件夹，则使用分号 (;) 来分隔文件夹。|  
|ASSOCIATED_MEASURE_GROUP|指定所有 MDX 计算应指向的度量值组名称的字符串。|  
  
 GOAL、STATUS 和 TREND 属性的值是 MDX 表达式，并且这些表达式的计算结果应该在 -1 和 1 之间。 但是，定义这些属性值的实际范围的是客户端应用程序。 当你使用的工具和客户端提供[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]若要浏览 Kpi，小于-1 的值将被视为-1，而大于 1 的值将被视为 1。  
  
 STATUS_GRAPHIC 和 TREND_GRAPHIC 都是字符串值，客户端应用程序使用它们来标识要显示的正确图像集。 这些字符串还定义显示函数的行为。 此行为包括要显示的状态数（通常是奇数），以及每种状态所使用的图像。  
  
### <a name="kpi-graphics-in-sql-server-data-tools"></a>SQL Server Data Tools 中的 KPI 图形  
 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，KPI 图形可以有三种或五种状态。 下表定义的每一种状态的值。  
  
|KPI 图形状态数|这些状态的值|  
|--------------------------------------|---------------------------|  
|3|差 = -1 到 -0.5<br /><br /> 正常 = 到 0.4999-0.4999<br /><br /> 好 = 0.50 到 1|  
|5|差 = -1 到 -0.75<br /><br /> 有风险 = -0.7499 到 -0.25<br /><br /> 一般 = -0.2499 到 0.2499<br /><br /> 良好 = 0.25 到 0.7499<br /><br /> 好 = 0.75 到 1|  
  
> [!NOTE]  
>  对于某些图形来说，如反向测量或反向状态箭头，则范围相反。 即，-1 是好，1 是差。  
  
 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，KPI 图形的名称可确定该图形有三种状态还是五种状态。 下表列出了使用情况、 名称和数字的指出[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]将其 KPI 图形与相关联。  
  
|图形用途|KPI 图形的名称|状态数|  
|--------------------|-------------------------|----------------------|  
|状态|形状|3|  
|状态|交通灯|3|  
|状态|路标|3|  
|状态|测量|3|  
|状态|反向测量|5|  
|状态|温度计|3|  
|状态|柱状|3|  
|状态|面|3|  
|状态|方差箭头|3|  
|走向|标准箭头|3|  
|走向|状态箭头|3|  
|走向|反向状态箭头|5|  
|走向|面|3|  
  
## <a name="see-also"></a>另请参阅  
 [删除 KPI 语句 &#40;MDX &#41;](../mdx/mdx-data-definition-drop-kpi.md)   
 [MDX 数据定义语句 &#40;MDX &#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
