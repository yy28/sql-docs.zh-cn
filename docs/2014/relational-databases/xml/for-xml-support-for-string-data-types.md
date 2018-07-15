---
title: 字符串数据类型的 FOR XML 支持 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- strings [SQL Server], XML
ms.assetid: bf069da8-de1e-44d2-a1fb-ade383076ac1
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3b81ccaf551f1d2a6d2a3edb106f45b8f9aa606f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37329317"
---
# <a name="for-xml-support-for-string-data-types"></a>字符串数据类型的 FOR XML 支持
  对数据中由 FOR XML 空格字符生成的 XML 进行实体化。  
  
 下面的示例创建了示例表 **T** ，并插入了包括 line feed、carriage return 和 tab 字符的示例数据。 SELECT 语句从表中检索数据。  
  
```  
CREATE TABLE T  
(  
  c1 int identity primary key,  
  c2 varchar(100)  
);  
go  
  
INSERT T (c2) VALUES ('Special character 0xD for carriage return ' + convert(varchar(10), 0xD) + ' after carriage return');  
INSERT T (c2) VALUES ('Special character 0x9 for tab ' + convert(varchar(10), 0x9) + ' after tab' );  
INSERT T (c2) VALUES ('Special character 0xA for line feed ' + convert(varchar(10), 0xA) + ' after line feed');  
go  
SELECT *   
FROM T  
FOR XML AUTO;  
go  
```  
  
 结果如下：  
  
```  
 <T c1="1" c2="Special character 0xD for carriage return   
 after carriage return" />  
 <T c1="2" c2="Special character 0x9 for tab     after tab" />  
 <T c1="3" c2="Special character 0xA for line feed   
after line feed" />  
```  
  
 请注意上述查询的以下方面：  
  
-   第一行中的 carriage return 被实体化为 &#xD。  
  
-   第二行中的 tab 被实体化为 &#x09。  
  
-   第三行中的 line feed 被实体化为 &#xA。  
  
## <a name="see-also"></a>请参阅  
 [各种 SQL Server 数据类型的 FOR XML 支持](for-xml-support-for-various-sql-server-data-types.md)  
  
  
