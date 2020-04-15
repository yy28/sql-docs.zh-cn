---
title: 设置 NULL 命令 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set nullSET NULL
ms.assetid: 410c5a6e-e957-4ecc-9e2d-e591cbc0bc4f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7c83c9ef9f8a0ce143308b73d8df09b05fb2cdea
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300807"
---
# <a name="set-null-command"></a>SET NULL 命令
确定 ALTER TABLE - SQL、创建表 - SQL 和 INSERT - SQL 命令支持空值的方式。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET NULL ON | OFF  
```  
  
## <a name="arguments"></a>参数  
 ON  
 （驱动程序的默认值;Visual FoxPro 的默认值为 OFF。指定使用 ALTER TABLE 和 CREATE TABLE 创建的表中的所有列都将允许空值。 通过在列的定义中包括"非 NULL"子句，可以覆盖表中列的 null 支持。  
  
 还指定 INSERT - SQL 将在插入插入插入 - SQL VALUE 子句中未包括的任何列中。 INSERT - SQL 将仅将空值插入允许空值的列中。  
  
 OFF  
 指定使用 ALTER TABLE 和 CREATE TABLE 创建的表中的所有列都不允许为空值。 通过在列的定义中包括 NULL 子句，可以为 ALTER TABLE 和 CREATE TABLE 中的列指定空值支持。  
  
 还指定 INSERT - SQL 将在插入"插入 - SQL VALUE"子句中未包括的任何列中插入空白值。  
  
## <a name="remarks"></a>备注  
 设置 NULL 仅影响 ALTER TABLE、创建表和插入 - SQL 支持空值的方式。 其他命令不受 SET NULL 的影响。  
  
## <a name="see-also"></a>另请参阅  
 [更改表 - SQL 命令](../../odbc/microsoft/alter-table-sql-command.md)   
 [创建表 - SQL 命令](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERT - SQL 命令](../../odbc/microsoft/insert-sql-command.md)
