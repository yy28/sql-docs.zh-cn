---
title: 为 Paradox 创建索引 |Microsoft Docs
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
ms.openlocfilehash: 331613676b748453a56da1e41fe85f04a7715038
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081941"
---
# <a name="create-index-for-paradox"></a>Paradox 的 CREATE INDEX
ODBC Paradox 驱动程序的 CREATE INDEX 语句的语法为：  
  
 **CREATE** [**UNIQUE**]**索引***索引名称*  
  
 **ON** *table name*  
  
 **（** *列标识符*[**ASC**]  
  
 [**，** *列标识符*[**ASC**] ...]**)**  
  
 ODBC Paradox 驱动程序不支持用于 CREATE INDEX 语句的 ODBC SQL 语法中的**DESC**关键字。 *表名*参数可以指定表的完整路径。  
  
 如果指定关键字**UNIQUE** ，则 ODBC Paradox 驱动程序将创建唯一索引。 第一个唯一索引创建为主索引。 这是一个名为 "*表名*" 的 Paradox 主密钥文件。像素. 主索引受到下列限制：  
  
-   必须先创建主索引，然后才能将任何行添加到表中。  
  
-   必须对表中的第一个 "n" 列定义主索引。  
  
-   每个表只允许有一个主索引。  
  
-   如果表上未定义主索引，则 Paradox 驱动程序无法更新表。 （请注意，对于空表，即使表中未定义唯一索引，也不能进行更新。）  
  
-   主索引的*索引名称*参数必须与表的基名称相同，因为 Paradox 是必需的。  
  
 如果省略关键字**UNIQUE** ，则 ODBC Paradox 驱动程序将创建一个不唯一的索引。 这包含两个名为 "*表名*" 的 Paradox 辅助索引文件。X*nn*和*表名称*。Y*nn*，其中*nn*是表中的列号。 非唯一索引受到以下限制：  
  
-   在为表创建非唯一索引之前，该表必须存在主索引。  
  
-   对于 Paradox 3。*x*：除主索引之外的任何索引（唯一或非唯一）的*索引名称*参数必须与列名称相同。 对于 Paradox 4。*x*和5。*x*，此类索引的名称可以是（但不一定）与列名称相同。  
  
-   只能为非唯一索引指定一列。  
  
 为表定义了索引后，就不能再添加列了。 如果 CREATE TABLE 语句的参数列表的第一列创建索引，则参数列表中不能包含第二列。  
  
 例如，若要使用销售订单号和行号列作为 SO_LINES 表上的唯一索引，请使用语句：  
  
```  
CREATE UNIQUE INDEX SO_LINES  
 ON SO_LINES (SONum, LineNum)  
```  
  
 若要使用 part number 列作为 SO_LINES 表中的非唯一索引，请使用语句：  
  
```  
CREATE INDEX PartNum  
 ON SO_LINES (PartNum)  
```  
  
 请注意，当执行两个 CREATE INDEX 语句时，第一条语句将始终创建一个与该表同名的主索引，第二个语句将始终使用与列相同的名称创建一个非唯一索引。 即使在 CREATE INDEX 语句中输入了不同的名称，并且在第二个 CREATE INDEX 语句中将索引标记为 UNIQUE，这些索引仍将以这种方式命名。  
  
> [!NOTE]  
>  如果在不实现 Borland 数据库引擎的情况下使用 Paradox 驱动程序，则只允许使用 read 和 append 语句。
