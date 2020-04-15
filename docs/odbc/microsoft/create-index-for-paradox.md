---
title: 为悖论创建索引 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2e68484efdc5194f93f2acab31973377d9c66f1c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280907"
---
# <a name="create-index-for-paradox"></a>Paradox 的 CREATE INDEX
ODBC 悖论驱动程序的 CREATE INDEX 语句的语法是：  
  
 **创建**=**唯一**=**索引***索引名称*  
  
 **打开***表名*  
  
 **（***列标识符*=**ASC**|  
  
 [**，** *列标识符*]**ASC**= ...**)**  
  
 ODBC 悖论驱动程序不支持 CREATE INDEX 语句的 ODBC SQL 语法中的**DESC**关键字。 *表名称*参数可以指定表的完整路径。  
  
 如果指定了关键字**UNIQUE，** 则 ODBC 悖论驱动程序将创建一个唯一索引。 第一个唯一索引创建为主索引。 这是一个名为*表名的*Paradox主键文件。Px。 主要索引受以下限制：  
  
-   必须先创建主索引，然后才能将任何行添加到表中。  
  
-   主索引必须定义在表中的第一个"n"列上。  
  
-   每个表只允许一个主索引。  
  
-   如果未在表上定义主索引，则 Paradox 驱动程序无法更新表。 （请注意，对于空表，这不是真的，即使表上未定义唯一索引，也可以更新空表。  
  
-   主索引的*索引名称*参数必须与表的基名相同，这是 Paradox 的要求。  
  
 如果省略关键字**UNIQUE**UNIQUE，ODBC 悖论驱动程序将创建一个非唯一索引。 这包括两个称为*表名*的 Paradox 辅助索引文件。X*nn*和*表名*。Y*nn*，其中*nn*是表中列的编号。 非唯一索引受以下限制：  
  
-   在为表创建非唯一索引之前，该表必须存在主索引。  
  
-   对于悖论3。*x*，主索引（唯一或非唯一）以外的任何索引*的索引名称*参数必须与列名称相同。 对于悖论4。*x*和 5。*x*，此类索引的名称可以是，但不必与列名称相同。  
  
-   只能为非唯一索引指定一列。  
  
 在表上定义索引后，无法添加列。 如果 CREATE TABLE 语句的参数列表的第一列创建索引，则第二列不能包含在参数列表中。  
  
 例如，要使用销售订单号和行号列作为SO_LINES表上的唯一索引，请使用语句：  
  
```  
CREATE UNIQUE INDEX SO_LINES  
 ON SO_LINES (SONum, LineNum)  
```  
  
 要将零件号列用作SO_LINES表上的非唯一索引，请使用 语句：  
  
```  
CREATE INDEX PartNum  
 ON SO_LINES (PartNum)  
```  
  
 请注意，执行两个 CREATE INDEX 语句时，第一个语句将始终创建与表同名的主索引，第二个语句将始终创建与列同名的非唯一索引。 即使在 CREATE INDEX 语句中输入了不同的名称，并且索引在第二个 CREATE INDEX 语句中标记为 UNIQUE，也会以这种方式命名这些索引。  
  
> [!NOTE]  
>  当您在不实现 Borland 数据库引擎的情况下使用 Paradox 驱动程序时，只允许读取和追加语句。
