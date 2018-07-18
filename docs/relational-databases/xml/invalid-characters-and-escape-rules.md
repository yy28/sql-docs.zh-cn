---
title: 无效字符和转义规则 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, invalid characters
- FOR XML clause, escape rules
ms.assetid: f2e9b997-f400-4963-b225-59d46c6b93e8
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6188f8359cb662ce7dc168d5e0745ebc8f53b722
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33013654"
---
# <a name="invalid-characters-and-escape-rules"></a>无效字符和转义规则
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  本主题介绍 FOR XML 子句如何处理无效的 XML 字符，并列出了在 XML 名称中无效的字符的转义规则。  
  
## <a name="for-xml-and-invalid-characters"></a>For XML 与无效字符  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 便会对这些字符进行实体化。  
  
 尽管 XML 1.0 一致性分析器不管这些字符是否被实体化都会生成分析错误，但是经过实体化的格式更符合 XML 1.1。 经过实体化的格式还可能更符合未来版本的 XML 标准。 此外，它使得调试变得更加简单，因为无效字符的码位将变为可见的。  
  
 对于 XML 工具的用户，不需要任何解决方法，因为无论怎样，在数据流中出现无效字符的位置，XML 分析器都将失败。 如果您使用非 XML 工具，则这种变化可能需要您更新编程逻辑以便将这些字符作为实体化后的值来搜索。  
  
 在 FOR XML 查询中以不同的方式来实体化下列空格字符，以使它们在整个往返中都存在：  
  
-   在元素内容和属性中： **hex(0D)** （回车符）  
  
-   在属性内容中： **hex(09)** （选项卡）、 **hex(0A)** （换行符）  
  
 输出中将保留这些字符，并且分析器将不再对它们进行规范。  
  
## <a name="escape-rules"></a>转义规则  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 名称转换成了 XML 名称。  
  
 只有两个非字母字符可以出现在 XML 名称中：冒号 (:) 和下划线 (_)。 由于冒号已经保留给命名空间，因此下划线被选作转义符。 以下是用于编码的转义规则：  
  
-   根据 XML 1.0 规范，任何不是有效的 XML 名称字符的 UCS-2 字符都将被转义为 _xHHHH\_。 HHHH 代表该字符对应的四位十六进制 UCS-2 代码，最重要的位排在最前面。 例如，表名 **Order Details** 被编码为 Order_x0020_Details。  
  
-   不适合 UCS-2 领域的字符（介于 U+00010000 到 U+0010FFFF 之间的附加 UCS-4 字符）均被编码为 _xHHHHHHHH\_。 如果处在 SQL Server 2000 向后兼容模式下，则 HHHHHHHH 代表该字符对应的八位十六进制 UCS-4 编码。 否则，会将字符编码为 _xHHHHHH\_，以便符合 ISO 标准。  
  
-   下划线字符不需要进行转义，除非其后为字符 x。 例如，表名 **Order_Details** 不进行编码。  
  
-   标识符中的冒号不进行转义，这样 FOR XML 查询就可以生成命名空间元素和属性名称。 例如，下面的查询将生成其名称中包含冒号的命名空间属性：  
  
    ```  
    SELECT 'namespace-urn' as 'xmlns:namespace',   
     1 as 'namespace:a'   
    FOR XML RAW  
    ```  
  
     此查询产生以下结果：  
  
    ```  
    <row xmlns:namespace="namespace-urn" namespace:a="1"/>  
    ```  
  
     请注意，建议使用 WITH XMLNAMESPACES 来添加 XML 命名空间。  
  
## <a name="see-also"></a>另请参阅  
 [FOR XML (SQL Server)](../../relational-databases/xml/for-xml-sql-server.md)  
  
  
