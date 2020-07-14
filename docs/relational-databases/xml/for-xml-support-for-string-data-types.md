---
title: 字符串数据类型的 FOR XML 支持 | Microsoft Docs
description: 了解 SQL 查询中 FOR XML 子句生成 XML 时，如何处理字符串数据类型。
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- strings [SQL Server], XML
ms.assetid: bf069da8-de1e-44d2-a1fb-ade383076ac1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cdaa7560b5dad561d981acee2d2d48ccca44146c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85729914"
---
# <a name="for-xml-support-for-string-data-types"></a>字符串数据类型的 FOR XML 支持
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
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
 [各种 SQL Server 数据类型的 FOR XML 支持](../../relational-databases/xml/for-xml-support-for-various-sql-server-data-types.md)  
  
  
