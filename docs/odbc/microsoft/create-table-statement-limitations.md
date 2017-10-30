---
title: "创建表语句限制 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CREATE TABLE statement limitations [ODBC]
- ODBC SQL grammar, CREATE TABLE statement limitations
ms.assetid: c5067855-20c9-456f-8d63-f375b4297f2e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0f7cec23f3ec8103b2805e0ee3c0f04d20011cb6
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="create-table-statement-limitations"></a>创建表语句的限制
当使用 Microsoft Access、 Microsoft Excel 或 Paradoxdriver 时，而且文本或二进制列的长度未指定 （或指定为 0），列长度将设置为 255。  
  
 当使用 dBASE 驱动程序时，和文本或二进制列的长度未指定 （或指定为 0），列长度将设置到 254 之间。  
  
 支持最多 255 列。  
  
 与以前删除工作表同名，无法创建 MicrosoftExcel 5.0，7.0 或 97 数据源，工作表上使用 Microsoft Excel 驱动程序时。 当 Microsoft Excel 驱动程序用于访问版本 5.0、 7.0 或 97 工作表时，DROP TABLE 语句将清除工作表中，但不会删除工作表的名称。  
  
 当使用 Paradox 驱动程序时，索引具有已定义的表后，不能添加列。 如果 CREATE TABLE 语句的自变量列表的第一列创建索引，第二列不能包含自变量列表中。

