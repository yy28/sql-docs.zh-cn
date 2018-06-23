---
title: 简单 XML 输入文件示例 (DTA) |Microsoft 文档
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
ms.assetid: 5b00e4eb-1742-43ec-98d8-d84216b6b840
caps.latest.revision: 21
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: a95a5c086d5c9c941407e6e3a92e2ea4f8cdcd72
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36025359"
---
# <a name="simple-xml-input-file-sample-dta"></a>简单 XML 输入文件示例 (DTA)
  将用于优化工作负荷的这一简单 XML 输入文件示例复制并粘贴到您喜爱的 XML 编辑器或文本编辑器中。 然后将为 **Server****Database****Schema**、**Table**、**Workload** 和 **TuningOptions** 元素指定的值替换为你的特定优化会话的值。 有关特性和可以与这些元素一起使用的子元素的详细信息，请参阅[XML 输入文件引用&#40;数据库引擎优化顾问&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)。 以下示例只使用了部分可用属性和子元素选项。  
  
## <a name="code"></a>代码  
 [!code-xml[InputFileSamples#SimpleXMLInputFile](../../snippets/xml/SQL14/dta_xml/inputfilesamples/xml/dta_xml_input_file_samples.xml#simplexmlinputfile)]  
  
## <a name="see-also"></a>请参阅  
 [启动并使用数据库引擎优化顾问](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)   
 [XML 输入文件引用（数据库引擎优化顾问）](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  