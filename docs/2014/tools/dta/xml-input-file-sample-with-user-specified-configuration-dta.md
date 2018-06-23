---
title: 使用用户指定配置的 XML 输入文件示例 (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- sample applications [DTA]
ms.assetid: b29c9716-e5c3-4003-9efb-3ade2197b630
caps.latest.revision: 18
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 933cae8582f104d9c70e608ab30ee938c8674175
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024464"
---
# <a name="xml-input-file-sample-with-user-specified-configuration-dta"></a>使用用户指定配置 (DTA) 的 XML 输入文件示例
  此 XML 输入文件示例使用 **Configuration** 元素来指定用户指定的配置，请将此示例文件复制并粘贴到你喜欢的 XML 编辑器或文本编辑器中。 这样将使您能够执行假设分析。 假设分析过程中将涉及使用 **Configuration** 元素为待优化的数据库指定一组假设的物理设计结构。 然后，可以使用数据库引擎优化顾问基于该假设配置对运行工作负荷进行效果分析，以查看它是否改进了查询处理性能。 此类分析具有的优点是，在评估新配置时不会引起实际实施它的开销。 如果假设配置未达到您期望的性能改进，则可以很容易的重新更改配置并进行分析，直到配置可以达到所需的结果。  
  
 将该示例输入文件复制到编辑工具中后，请将为 **Server**、 **Database**、 **Schema**、 **Table**、 **Workload**、 **TuningOptions**和 **Configuration** 元素指定的值替换为具体的优化会话的值。 有关的所有属性和可以与这些元素一起使用的子元素的详细信息，请参阅[XML 输入文件引用&#40;数据库引擎优化顾问&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)。 以下示例只使用了部分可用属性和子元素选项。  
  
## <a name="code"></a>代码  
 [!code-xml[InputFileSamples#UserSpecifiedConfigInputFile](../../snippets/xml/SQL14/dta_xml/inputfilesamples/xml/dta_xml_input_file_samples.xml#userspecifiedconfiginputfile)]  
  
## <a name="comments"></a>注释  
  
-   如果为 **Configuration** 元素指定 **Absolute** 模式 (`Configuration SpecificationMode="Absolute"`)，则将无法删除物理设计结构。  
  
-   不能在**Configuration** 元素的任何一个模式（ **Relative**或 **Absolute** ）中创建并删除同一个物理设计结构。  
  
## <a name="see-also"></a>请参阅  
 [启动并使用数据库引擎优化顾问](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)   
 [查看和使用数据库引擎优化顾问的输出](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)   
 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  