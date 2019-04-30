---
title: CREATE INDEX for Paradox | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX [ODBC]
- Paradox driver [ODBC], create index
ms.assetid: 6472bd69-b931-4bc2-a9bf-f1873ed4cdfe
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 15e16fb311bf3c9acb2823772247e0fc16eabeef
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63232304"
---
# <a name="create-index-for-paradox"></a>Paradox 的 CREATE INDEX
ODBC Paradox 驱动程序的 CREATE INDEX 语句的语法是：  
  
 **CREATE** [**UNIQUE**] **INDEX** *index-name*  
  
 **ON** *table-name*  
  
 **(** *column-identifier* [**ASC**]  
  
 [**,** *column-identifier* [**ASC**]...]**)**  
  
 ODBC Paradox 驱动程序不支持**DESC** ODBC SQL 语法的 CREATE INDEX 语句中的关键字。 *表名称*参数可指定表的完整路径。  
  
 如果关键字**UNIQUE** ODBC Paradox 驱动程序将创建唯一索引的指定。 第一个唯一索引作为主索引创建。 这是名为 Paradox 主要密钥文件*表名称*。像素。 主索引是有以下限制：  
  
-   任何行添加到表之前，必须创建主索引。  
  
-   在表中的第一个"n"列时，必须定义主索引。  
  
-   只有一个主索引允许每个表中。  
  
-   如果未对表定义主索引，则不能通过 Paradox 驱动程序更新的表。 （请注意，这不是为一个空表，它可以更新，即使未对表定义唯一索引，则返回 true。）  
  
-   *索引名称*参数的主索引必须是表中，所需的 Paradox 的基名称相同。  
  
 如果关键字**UNIQUE**是省略，ODBC Paradox 驱动程序将创建非唯一索引。 这两个名为的 Paradox 辅助索引文件组成*表名称*。X*nn*并*表名*。Y*nn*，其中*nn*是表中的列数。 非唯一索引受到以下限制：  
  
-   可以为表创建非唯一索引之前，该表必须存在主索引。  
  
-   可能是 3。*x*，则*索引名称*参数的主索引 （唯一或非唯一） 之外的任何索引必须是列名称相同。 可能是 4。*x*和 5。*x*，此类索引的名称可以但不一定是列名称相同。  
  
-   为非唯一索引，可以指定只有一个列。  
  
 在表上定义索引后，无法添加列。 如果 CREATE TABLE 语句的参数列表的第一列创建索引，第二个列不能包含参数列表中。  
  
 例如，若要使用的销售订单号和行号列作为 SO_LINES 表的唯一索引，使用该语句：  
  
```  
CREATE UNIQUE INDEX SO_LINES  
 ON SO_LINES (SONum, LineNum)  
```  
  
 若要将部件号列用作 SO_LINES 表的非唯一索引，使用该语句：  
  
```  
CREATE INDEX PartNum  
 ON SO_LINES (PartNum)  
```  
  
 请注意，当执行两个 CREATE INDEX 语句时，第一条语句将始终创建主索引与表相同的名称与第二个语句将始终具有相同名称的列创建非唯一索引。 这些索引名称将为这种方式即使 CREATE INDEX 语句中输入不同的名称，即使索引 UNIQUE 标记为在第二个 CREATE INDEX 语句中。  
  
> [!NOTE]  
>  当使用 Paradox 驱动程序而无需实现 borland 公司数据库引擎，只读取和追加允许语句。
