---
title: "FOR JSON 如何转义特殊字符和控制字符 (SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "FOR JSON, 特殊字符"
ms.assetid: 4ba90025-5a09-4f0a-836a-54c886324530
caps.latest.revision: 16
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# FOR JSON 如何转义特殊字符和控制字符 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  本主题介绍 **FOR JSON** 子句如何在 JSON 输出中转义特殊字符和表示控制字符。  
  
## 特殊字符转义  
 **FOR JSON** 子句使用 `\` 在 JSON 输出中转义特殊字符，如下表所示。 在属性名称及其值中，均会发生这种转义。  
  
|**特殊字符**|**编码的序列**|  
|---------------------------|--------------------------|  
|引号 (")|\\"|  
|反斜杠 (\\)|\\\|  
|正斜杠 (/)|\\/|  
|退格键|\b|  
|换页符|\f|  
|换行符|\n|  
|回车符|\r|  
|水平制表符|\t|  
  
## 控制字符  
 **FOR JSON** 子句使用 `\u<code>` 格式在 JSON 输出中表示控制字符，如下表所示。  
  
|**控制字符**|**编码的序列**|  
|---------------------------|--------------------------|  
|CHAR(0)|\u0000|  
|CHAR(1)|\u0001|  
|…|…|  
|CHAR(31)|\u001f|  
  
## 示例  
 下面是一个 **FOR JSON** 子句示例，其中包括转义和控制字符。  
  
 查询：  
  
```tsql  
SELECT  
  'VALUE\    /  
  "' as [KEY\/"],  
  CHAR(0) as '0',  
  CHAR(1) as '1',  
  CHAR(31) as '31'  
FOR JSON PATH  
```  
  
 结果：  
  
```json  
{  
   "KEY\\\t\/\"":"VALUE\\\t\/\r\n\"",  
   "0":"\u0000",  
   "1":"\u0001",  
  "31":"\u001f“  
}  
```  
  
## 另请参阅  
 [借助 FOR JSON 将查询结果的格式设置为 JSON (SQL Server)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  