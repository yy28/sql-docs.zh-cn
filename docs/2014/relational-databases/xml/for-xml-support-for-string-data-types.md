---
title: 字符串数据类型的 FOR XML 支持 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- strings [SQL Server], XML
ms.assetid: bf069da8-de1e-44d2-a1fb-ade383076ac1
author: rothja
ms.author: jroth
ms.openlocfilehash: b768f963f4b905d9d7e5a1004247b305c132262a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059452"
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
  
## <a name="see-also"></a>另请参阅  
 [各种 SQL Server 数据类型的 FOR XML 支持](for-xml-support-for-various-sql-server-data-types.md)  
  
  
