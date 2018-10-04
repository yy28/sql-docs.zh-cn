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
manager: craigg
ms.openlocfilehash: f5eab1c3bf6891f10c897966035dced2ffdc10ba
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622105"
---
# <a name="create-table-statement-limitations"></a>CREATE TABLE 语句限制
使用 Microsoft Access、 Microsoft Excel 或 Paradoxdriver 时，和未指定的文本或二进制列长度 （或指定为 0），列长度将设置为 255。  
  
 当使用 dBASE 驱动程序时，和未指定的文本或二进制列长度 （或指定为 0），列长度将设置为 254。  
  
 支持最多为 255 列。  
  
 使用与以前删除的工作表相同的名称，不能创建 MicrosoftExcel 5.0、 7.0、 或 97 数据源，工作表上使用 Microsoft Excel 驱动程序时。 当 Microsoft Excel 驱动程序用于访问版本 5.0、 7.0、 或 97 工作表时，DROP TABLE 语句清除工作表中，但不会删除工作表名称。  
  
 当使用 Paradox 驱动程序时，表上定义索引后不能添加列。 如果 CREATE TABLE 语句的参数列表的第一列创建索引，第二个列不能包含参数列表中。
