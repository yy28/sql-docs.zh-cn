---
title: CREATE TABLE 语句限制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE TABLE statement limitations [ODBC]
- ODBC SQL grammar, CREATE TABLE statement limitations
ms.assetid: c5067855-20c9-456f-8d63-f375b4297f2e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db5d2cb8decde9828acd3005551717ac9f6cef32
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096596"
---
# <a name="create-table-statement-limitations"></a>CREATE TABLE 语句限制
当使用 Microsoft Access、Microsoft Excel 或 Paradoxdriver 时，如果未指定 text 或 binary 列的长度（或指定为0），则列长度将设置为255。  
  
 使用 dBASE 驱动程序时，如果未指定 text 或 binary 列的长度（或指定为0），则列长度将设置为254。  
  
 最多支持255列。  
  
 当在 MicrosoftExcel 5.0、7.0 或97数据源上使用 Microsoft Excel 驱动程序时，不能创建与先前删除的工作表同名的工作表。 当使用 Microsoft Excel 驱动程序访问版本5.0、7.0 或97工作表时，DROP TABLE 语句会清除工作表，但不会删除工作表名称。  
  
 使用 Paradox 驱动程序时，一旦对表定义了索引，将无法添加列。 如果 CREATE TABLE 语句的参数列表的第一列创建索引，则参数列表中不能包含第二列。
