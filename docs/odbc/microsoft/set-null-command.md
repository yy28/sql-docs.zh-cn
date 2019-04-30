---
title: SET NULL 命令 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b6f0e23abd31661210282967fa35080376eaaaf3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63159303"
---
# <a name="set-null-command"></a>SET NULL 命令
确定如何 null 值支持的 ALTER TABLE-SQL、 CREATE TABLE-SQL 和 INSERT-SQL 命令。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET NULL ON | OFF  
```  
  
## <a name="arguments"></a>参数  
 ON  
 （默认为驱动程序，Visual FoxPro 的默认值为 OFF。）指定创建与 ALTER TABLE 和 CREATE TABLE 的表中的所有列都允许 null 值。 您可以通过在这些列的定义中包含 NOT NULL 子句覆盖表中的列的 null 值支持。  
  
 此外指定 INSERT-SQL 将插入 null 值到 INSERT-SQL VALUE 子句中不包含任何列。 INSERT-SQL 将插入 null 值仅允许 null 值的列。  
  
 OFF  
 指定创建与 ALTER TABLE 和 CREATE TABLE 的表中的所有列将不都允许 null 值。 也可以通过在这些列的定义中包括 NULL 子句指定 ALTER TABLE 和 CREATE TABLE 中的列的 null 值支持。  
  
 此外指定 INSERT-SQL 将插入空值为 INSERT-SQL VALUE 子句中不包含任何列。  
  
## <a name="remarks"></a>备注  
 通过 ALTER TABLE、 CREATE TABLE 和 INSERT-SQL 支持设置为 NULL 的会影响仅如何 null 值。 其他命令不受 SET NULL。  
  
## <a name="see-also"></a>请参阅  
 [ALTER TABLE-SQL 命令](../../odbc/microsoft/alter-table-sql-command.md)   
 [CREATE TABLE-SQL 命令](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERT - SQL 命令](../../odbc/microsoft/insert-sql-command.md)
