---
title: CREATE KPI 语句（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e2380f72fe8a5faf9dc5504e56941f724b1bd159
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68098402"
---
# <a name="mdx-data-definition---create-kpi"></a>MDX 数据定义 - CREATE KPI


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
  
## <a name="remarks"></a>备注  
 指定当前连接的多维数据集以外的多维数据集将导致错误。 因此，应使用 CURRENTCUBE 来代替多维数据集名称，以表示当前的多维数据集。  
  
## <a name="kpi-properties"></a>KPI 属性  
 下表列出了所有的 KPI 属性。 这些属性都没有默认值。 因此，在为 KPI 属性指定某个特定值之前，针对该属性的查询会返回空值。  
  
|属性标识符|含义|  
|-------------------------|-------------|  
|GOAL|返回数值的有效 MDX 表达式。|  
|状态|返回数值的有效 MDX 表达式。|  
|STATUS_GRAPHIC|用于定义一组图形图像的字符串，这些图形图像将由客户端应用程序使用。|  
|TREND|返回数值的有效 MDX 表达式。|  
|TREND_GRAPHIC|用于定义一组图形图像的字符串，这些图形图像将由客户端应用程序使用。|  
|WEIGHT|返回数值的有效 MDX 表达式。|  
|CURRENT_TIME_MEMBER|返回时间维度成员的有效 MDX 表达式。 CURRENT_TIME_MEMBER 设置所有相对时间函数的参考点|  
|PARENT_KPI|指定父级 KPI 名称的字符串。|  
|CAPTION|客户端应用程序用作 KPI 标题的字符串。|  
|DISPLAY_FOLDER|指定显示文件夹的路径的字符串，客户端应用程序将在此处显示 KPI。 文件夹级别的分隔符由客户端应用程序定义。 对于提供的工具和客户端[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，反斜杠（\\）是级别分隔符。 若要为已定义的成员提供多个显示文件夹，则使用分号 (;) 来分隔文件夹。|  
|ASSOCIATED_MEASURE_GROUP|指定所有 MDX 计算应指向的度量值组名称的字符串。|  
  
 GOAL、STATUS 和 TREND 属性的值是 MDX 表达式，并且这些表达式的计算结果应该在 -1 和 1 之间。 但是，定义这些属性值的实际范围的是客户端应用程序。 使用提供的[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]工具和客户端浏览 kpi 时，小于-1 的值将被视为-1，大于1的值将被视为1。  
  
 STATUS_GRAPHIC 和 TREND_GRAPHIC 都是字符串值，客户端应用程序使用它们来标识要显示的正确图像集。 这些字符串还定义显示函数的行为。 此行为包括要显示的状态数（通常是奇数），以及每种状态所使用的图像。  
  
### <a name="kpi-graphics-in-sql-server-data-tools"></a>SQL Server Data Tools 中的 KPI 图形  
 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，KPI 图形可以有三种或五种状态。 下表定义了每种状态的值。  
  
|KPI 图形状态数|这些状态的值|  
|--------------------------------------|---------------------------|  
|3|差 = -1 到 -0.5<br /><br /> 正常 =-0.4999 到0.4999<br /><br /> 好 = 0.50 到 1|  
|5|差 = -1 到 -0.75<br /><br /> 有风险 = -0.7499 到 -0.25<br /><br /> 一般 = -0.2499 到 0.2499<br /><br /> 良好 = 0.25 到 0.7499<br /><br /> 好 = 0.75 到 1|  
  
> [!NOTE]  
>  对于某些图形来说，如反向测量或反向状态箭头，则范围相反。 即，-1 是好，1 是差。  
  
 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，KPI 图形的名称可确定该图形有三种状态还是五种状态。 下表列出了与 KPI 图形[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]关联的状态、名称和状态数。  
  
|图形用途|KPI 图形的名称|状态数|  
|--------------------|-------------------------|----------------------|  
|状态|形状|3|  
|状态|交通灯|3|  
|状态|路标|3|  
|状态|仪表|3|  
|状态|反向测量|5|  
|状态|温度计|3|  
|状态|柱状|3|  
|状态|面|3|  
|状态|方差箭头|3|  
|趋势|标准箭头|3|  
|趋势|状态箭头|3|  
|趋势|反向状态箭头|5|  
|趋势|面|3|  
  
## <a name="see-also"></a>另请参阅  
 [DROP KPI 语句 &#40;MDX&#41;](../mdx/mdx-data-definition-drop-kpi.md)   
 [Mdx 数据定义语句 &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
