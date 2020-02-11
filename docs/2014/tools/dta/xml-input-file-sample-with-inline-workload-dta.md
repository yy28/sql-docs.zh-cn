---
title: 内联工作负荷的 XML 输入文件示例 (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- sample applications [DTA]
ms.assetid: 7c04fe1d-6669-44a1-8b73-36d469e9b002
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b1b53076a7528d0e9eaff1244c206dee4127150e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63063133"
---
# <a name="xml-input-file-sample-with-inline-workload-dta"></a>内联工作负荷的 XML 输入文件示例 (DTA)
  将使用**EventString**元素指定工作负荷的 xml 输入文件示例复制并粘贴到常用的 XML 编辑器或文本编辑器。 您可以在 XML 输入文件中使用 **EventString** 元素指定一个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本工作负荷，而不必使用单独的工作负荷文件。 将此示例复制到编辑工具中后，将为 **服务器**、 **数据库**、 **架构**、 **表**、 **工作负荷**、 **EventString**和 **TuningOptions** 元素指定的值，替换为具体的优化会话所用的值。 有关可以与这些元素一起使用的所有属性和子元素的详细信息，请参阅 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)。 以下示例只使用了部分可用属性和子元素选项。  
  
## <a name="code"></a>代码  
 [!code-xml[InputFileSamples#InlineWorkloadInputFile](../../snippets/xml/SQL14/dta_xml/inputfilesamples/xml/dta_xml_input_file_samples.xml#inlineworkloadinputfile)]  
  
## <a name="comments"></a>注释  
 `USE database_name`语句可以在包含在**EventString**元素中的内联工作负荷中指定。  
  
## <a name="see-also"></a>另请参阅  
 [启动并使用数据库引擎优化顾问](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)   
 [查看并使用数据库引擎优化顾问的输出](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)   
 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
