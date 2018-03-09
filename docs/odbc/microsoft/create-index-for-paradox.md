---
title: "为 Paradox 创建索引 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CREATE INDEX [ODBC]
- Paradox driver [ODBC], create index
ms.assetid: 6472bd69-b931-4bc2-a9bf-f1873ed4cdfe
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a64feb77cc0562635b5e432174c58503e459e8ba
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="create-index-for-paradox"></a>为 Paradox 创建索引
ODBC Paradox 驱动程序的 CREATE INDEX 语句的语法是：  
  
 **创建**[**UNIQUE**]**索引***索引名称*  
  
 **ON** *表名称*  
  
 **(** *列标识符*[**ASC**]  
  
 [**，** *列标识符*[**ASC**]...]**)**  
  
 ODBC Paradox 驱动程序不支持**DESC** CREATE INDEX 语句的 ODBC SQL 语法中的关键字。 *表名*自变量可以指定表的完整路径。  
  
 如果关键字**UNIQUE** ODBC Paradox 驱动程序将创建唯一索引的指定。 第一个唯一索引作为主索引创建。 这是名为的一个 Paradox 主密钥文件*表名*。PX。 主索引受到以下限制：  
  
-   在任何行添加到表之前，必须创建主索引。  
  
-   在表中的第一个"n"列时，必须定义主索引。  
  
-   只有一个主索引允许每个表中。  
  
-   表不能通过 Paradox 驱动程序更新，如果未对表定义主索引。 （请注意这不是最适用于一个空表，它可以更新，即使未在表上定义唯一索引。）  
  
-   *索引名称*主索引的参数必须为表中，根据需要通过 Paradox 的基名称相同。  
  
 如果关键字**UNIQUE**是省略，ODBC Paradox 驱动程序将创建非唯一索引。 这包括名为的两个 Paradox 辅助索引文件*表名*。X *nn* 和*表名*。Y*nn*，其中 *nn* 是表中的列数。 非唯一索引受到以下限制：  
  
-   可以对表创建非唯一索引之前，该表必须存在主索引。  
  
-   可能是 3。*x*、*索引名称*主索引 （唯一或非唯一） 以外的任何索引的参数必须是列名称相同。 可能是 4。*x*和 5。*x*，此类索引的名称可以是，但不一定是，列名称相同。  
  
-   为非唯一索引，可以指定只有一个列。  
  
 一旦在表上定义索引，不能添加列。 如果 CREATE TABLE 语句的自变量列表的第一列创建索引，第二列不能包含自变量列表中。  
  
 例如，若要使用销售订单号和行号列作为 SO_LINES 表的唯一索引，请使用语句：  
  
```  
CREATE UNIQUE INDEX SO_LINES  
 ON SO_LINES (SONum, LineNum)  
```  
  
 若要使用的部件号列作为 SO_LINES 表上的非唯一索引，请使用语句：  
  
```  
CREATE INDEX PartNum  
 ON SO_LINES (PartNum)  
```  
  
 请注意时执行两个 CREATE INDEX 语句，第一个语句将始终创建主索引具有与表相同的名称和第二个语句将始终创建非唯一索引具有与列相同的名称。 这些索引将进行命名这种方式，即使在 CREATE INDEX 语句中输入不同名称，即使索引标记 UNIQUE 为第二个 CREATE INDEX 语句中。  
  
> [!NOTE]  
>  当你使用 Paradox 驱动程序，而无需实现高数据库引擎，仅读取并追加允许语句。
