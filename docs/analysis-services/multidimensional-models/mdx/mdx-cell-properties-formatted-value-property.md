---
title: "基于 LANGUAGE 和 FORMAT_STRING 上 FORMATTED_VALUE |Microsoft 文档"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7534ff5f-954e-47d4-a2ed-4b5b8ccb30e6
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 465b5ce3730dc73357502ff88517eb3c5dd29d20
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="mdx-cell-properties---formattedvalue-property"></a>MDX 单元格属性-FORMATTED_VALUE 属性
  FORMATTED_VALUE 属性是基于单元的 VALUE、FORMAT_STRING 和 LANGUAGE 属性的交互生成的。 本主题说明这些属性通过何种方式进行交互来生成 FORMATTED_VALUE 属性。  
  
## <a name="value-formatstring-language-properties"></a>VALUE、FORMAT_STRING、LANGUAGE 属性  
 下表说明了这些属性的定义，可为我们将来合并使用这些属性提供帮助。  
  
 VALUE  
 单元的未格式化值。  
  
 FORMAT_STRING  
 将应用于单元的值以生成 FORMATTED_VALUE 属性的格式模板。  
  
 LANGUAGE  
 要与 FORMAT_STRING 一起应用以生成本地化版本的 FORMATTED_VALUE 的区域设置规范。  
  
## <a name="formattedvalue-constructed"></a>FORMATTED_VALUE 的构造  
 FORMATTED_VALUE 属性是通过使用 VALUE 属性中的值并对该值应用 FORMAT_STRING 属性中指定的格式模板构造而成。 另外，每当格式值为 **命名的格式文字** 时，LANGUAGE 属性规范便会修改 FORMAT_STRING 的输出结果以遵守命名格式的语言用法。 所有命名格式文字都定义为可本地化。 例如， `"General Date"` 为可以本地化的规范，而下面的模板 `"YYYY-MM-DD hh:nn:ss",` 则相反，该模板指定所显示的日期由模板定义，与语言规范无关。  
  
 如果 FORMAT_STRING 模板和 LANGUAGE 规范之间有冲突，则 FORMAT_STRING 模板将优先于 LANGUAGE 规范。 例如，如果指定 FORMAT_STRING="$ #0" 且 LANGUAGE=1034（西班牙），VALUE=123.456，则 FORMATTED_VALUE="$ 123" 而不是 FORMATTED_VALUE="€ 123"（期望的格式为欧元），因为格式模板的值优先于指定的语言。  
  
### <a name="examples"></a>示例  
 以下示例显示了将 LANGUAGE 与 FORMAT_STRING 合并使用时获得的输出结果。  
  
 第一个示例说明了数字值的格式设置；第二个示例说明了日期和时间值的格式设置。  
  
 对每个示例均指定了多维表达式 (MDX) 代码。  
  
 `with`  
  
 `member measures.A as 5040, FORMAT_STRING="Currency"`  
  
 `member measures.B as measures.A, LANGUAGE=1034`  
  
 `member measures.C as measures.A, LANGUAGE=1034 , FORMAT_STRING="$#,##0.00"`  
  
 `member measures.D as measures.A, FORMAT_STRING="Scientific"`  
  
 `member measures.E as measures.A, LANGUAGE=1034 , FORMAT_STRING="Scientific"`  
  
 `member measures.F as 0.5040, FORMAT_STRING="Percent"`  
  
 `member measures.G as measures.F, LANGUAGE=1034`  
  
 `member measures.H as 0, LANGUAGE=1034 , FORMAT_STRING="Yes/No"`  
  
 `member measures.I as 59, LANGUAGE=1034 , FORMAT_STRING="Yes/No"`  
  
 `member measures.J as 0, LANGUAGE=1034 , FORMAT_STRING="ON/OFF"`  
  
 `member measures.K as -312, LANGUAGE=1034 , FORMAT_STRING="ON/OFF"`  
  
 `Select {measures.A, measures.B, measures.C, measures.D, measures.E, measures.F, measures.G, measures.H, measures.I, measures.J, measures.K} on 0`  
  
 `from [Adventure Works]`  
  
 `cell properties VALUE, FORMAT_STRING, LANGUAGE, FORMATTED_VALUE`  
  
 使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在区域设置为 1033 的服务器和客户端上运行上述 MDX 查询时，转置后的结果为如下所示：  
  
|成员|FORMATTED_VALUE|解释|  
|------------|----------------------|-----------------|  
|指向|$5,040.00|FORMAT_STRING 设置为 `Currency` ，LANGUAGE 为从系统区域设置值继承的 `1033`|  
|B|€5.040,00|FORMAT_STRING 设置为 `Currency` （从 A 继承），并且 LANGUAGE 显式设置为 `1034` （西班牙），因此显示的是欧元符号，所使用的小数分隔符和千分分隔符也与前面的示例不相同。|  
|C|$5.040,00|FORMAT_STRING 设置为 `$#,##0.00` ，取代了来自 A 的 Currency，并且 LANGUAGE 显式设置为 `1034` （西班牙）。 因为 FORMAT_STRING 属性将货币符号显式设置为 $，因此 FORMATTED_VALUE 将使用 $ 符号显示。 然而，因为 `.` （点）和 `,` （逗号）分别为小数分隔符和千位分隔符的占位符，因此该语言规范将对这些占位符所生成的小数点分隔符和千位分隔符的本地化输出结果产生影响。|  
|D|5.04E+03|FORMAT_STRING 设置为 `Scientific` ，LANGUAGE 设置为从系统区域设置值继承的 `1033`，因此以 `.` （点）作为小数分隔符。|  
|E|5,04E+03|FORMAT_STRING 设置为 `Scientific` ，LANGUAGE 显式设置为 `1034,` ，因此以 `,` （逗号）作为小数分隔符。|  
|F|50.40%|FORMAT_STRING 设置为 `Percent` ，LANGUAGE 设置为从系统区域设置值继承的 `1033`，因此以 `.` （点）作为小数分隔符。<br /><br /> 请注意，VALUE 已从 5040 更改为 0.5040|  
|G|50,40%|FORMAT_STRING 设置为 `Percent`（从 F 继承），LANGUAGE 显式设置为 `1034` ，因此以 `,` （逗号）作为小数点分隔符。<br /><br /> 请注意，VALUE 从 F 的值继承。|  
|H|“否”|FORMAT_STRING 设置为 `YES/NO`，VALUE 设置为 0，并且 LANGUAGE 显式设置为 `1034`；因为英语 NO 和西班牙语 NO 之间并无区别，因此用户在 FORMATTED_VALUE 中看不到任何差别。|  
|I|SI|FORMAT_STRING 设置为 `YES/NO`，VALUE 设置为 59，并且 LANGUAGE 显式设置为 `1034`；根据针对 YES/NO 格式设置的定义，任何零 (0) 以外的值均为 YES，并且因为语言设置为西班牙语，所以 FORMATTED_VALUE 为 SI。|  
|J|Desactivado|FORMAT_STRING 设置为 `ON/OFF`，VALUE 设置为 0，并且 LANGUAGE 显式设置为 `1034`；根据针对 ON/OFF 格式设置的定义，任何等于零 (0) 的值均为 OFF，并且因为语言设置为西班牙语，因此 FORMATTED_VALUE 为 Desactivado。|  
|K|Activado|FORMAT_STRING 设置为 `ON/OFF`，VALUE 设置为 -312，并且 LANGUAGE 显式设置为 `1034`；根据针对 ON/OFF 格式设置的定义，任何零 (0) 以外的值均为 ON，并且因为语言设置为西班牙语，因此 FORMATTED_VALUE 为 Activado。|  
  
 `with`  
  
 `member measures.A as 'CDate("1959-03-12 06:30")'`  
  
 `member measures.B as measures.A, FORMAT_STRING="Long Date"`  
  
 `member measures.C as measures.A, LANGUAGE=1034 , FORMAT_STRING="General Date"`  
  
 `member measures.D as measures.A, LANGUAGE=1034, FORMAT_STRING="Long Date"`  
  
 `member measures.E as measures.A, LANGUAGE=1041 , FORMAT_STRING="General Date"`  
  
 `member measures.F as measures.A, LANGUAGE=1041 , FORMAT_STRING="Long Date"`  
  
 `member measures.G as measures.A, FORMAT_STRING="Long Time"`  
  
 `member measures.H as measures.A, FORMAT_STRING="Short Time"`  
  
 `member measures.I as measures.A, LANGUAGE=1034 , FORMAT_STRING="Long Time"`  
  
 `member measures.J as measures.A, LANGUAGE=1034 , FORMAT_STRING="Short Time"`  
  
 `member measures.K as measures.A, LANGUAGE=1041 , FORMAT_STRING="Long Time"`  
  
 `member measures.L as measures.A, LANGUAGE=1041 , FORMAT_STRING="Short Time"`  
  
 `Select {measures.A, measures.B, measures.C, measures.D, measures.E, measures.F`  
  
 `, measures.G, measures.H, measures.I, measures.J, measures.K, measures.L} on 0`  
  
 `from [Adventure Works]`  
  
 `cell properties VALUE, FORMAT_STRING, LANGUAGE, FORMATTED_VALUE`  
  
 使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在区域设置为 1033 的服务器和客户端上运行上述 MDX 查询时，转置后的结果为如下所示：  
  
|成员|FORMATTED_VALUE|解释|  
|------------|----------------------|-----------------|  
|指向|3/12/1959 6:30:00 AM|FORMAT_STRING 通过 CDate() 表达式隐式设置为 `General Date` ，并且 LANGUAGE 为从系统区域设置值继承的 `1033` （英语）|  
|B|Thursday, March 12, 1959|FORMAT_STRING 显式设置为 `Long Date` ，并且 LANGUAGE 为从系统区域设置值继承的 `1033` （英语）|  
|C|12/03/1959 6:30:00|FORMAT_STRING 显式设置为 `General Date` ，并且 LANGUAGE 为显式 `1034` （西班牙语）。<br /><br /> 请注意，在与美国格式设置样式进行比较时应切换月和天|  
|D|jueves, 12 de marzo de 1959|FORMAT_STRING 显式设置为 `Long Date` ，并且 LANGUAGE 为显式 `1034` （西班牙语）。<br /><br /> 请注意月和星期是用西班牙语拼写的|  
|E|1959/03/12 6:30:00|FORMAT_STRING 显式设置为 `General Date` ，并且 LANGUAGE 为显式 `1041` （日语）。<br /><br /> 请注意，现在的日期格式设置为：年/月/日 小时:分钟:秒钟|  
|F|1959年3月12日|FORMAT_STRING 显式设置为 `Long Date` ，并且 LANGUAGE 为显式 `1041` （日语）。|  
|G|6:30:00 AM|FORMAT_STRING 显式设置为 `Long Time` ，并且 LANGUAGE 为从系统区域设置值继承的 `1033` （英语）。|  
|H|06:30|FORMAT_STRING 显式设置为 `Short Time` ，并且 LANGUAGE 为从系统区域设置值继承的 `1033` （英语）。|  
|I|6:30:00|FORMAT_STRING 显式设置为 `Long Time` ，并且 LANGUAGE 显式设置为 `1034` （西班牙语）。|  
|J|06:30|FORMAT_STRING 显式设置为 `Short Time` ，并且 LANGUAGE 显式设置为 `1034` （西班牙语）。|  
|K|6:30:00|FORMAT_STRING 显式设置为 `Long Time` ，并且 LANGUAGE 显式设置为 `1041` （日语）。|  
|L|06:30|FORMAT_STRING 显式设置为 `Short Time` ，并且 LANGUAGE 显式设置为 `1041` （日语）。|  
  
## <a name="see-also"></a>另请参阅  
 [FORMAT_STRING 内容 (MDX)](../../../analysis-services/multidimensional-models/mdx/mdx-cell-properties-format-string-contents.md)   
 [使用单元属性 &#40;MDX &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-properties-using-cell-properties.md)   
 [创建和使用属性值 &#40;MDX &#41;](http://msdn.microsoft.com/library/0cafb269-03c8-4183-b6e9-220f071e4ef2)   
 [MDX 查询基础知识 (Analysis Services)](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  

