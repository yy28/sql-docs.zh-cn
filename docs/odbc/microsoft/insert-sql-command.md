---
title: INSERT-SQL 命令 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- INSERT [ODBC]
ms.assetid: 9b648198-349f-46f6-b869-13d129945971
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 884a33339db10ee8e07d8b432d1765720d45734a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019448"
---
# <a name="insert---sql-command"></a>INSERT - SQL 命令
包含指定的字段值的表的末尾追加一条记录。  
  
 Visual FoxPro ODBC 驱动程序支持本机 Visual FoxPro 语言语法，此命令。 特定于驱动程序的信息，请参阅备注。  
  
## <a name="syntax"></a>语法  
  
```  
  
INSERT INTO dbf_name [(fname1 [, fname2, ...])]  
   VALUES (eExpression1 [, eExpression2, ...])  
```  
  
## <a name="arguments"></a>参数  
 INSERT INTO *dbf_name*  
 指定新的记录追加到的表的名称。 *dbf_name*可以包含路径，可以是名称表达式。  
  
 如果您指定的表未打开，在新的工作区中以独占方式打开和新的记录追加到表。 未选择新的工作区域;当前工作区处于选定状态。  
  
 如果打开指定的表，INSERT 将新记录追加到表。 如果表是在工作区中打开，而不是当前工作区，它不被选择后追加记录;当前工作区处于选定状态。  
  
 [( *fname1*[， *fname2*[，...]])]  
 新记录中指定的字段的名称值将插入到。  
  
 值 ( *eExpression1*[， *eExpression2*[，...]])  
 指定插入新记录的字段值。 如果省略的字段名称，必须由表结构定义的顺序来指定字段值。  
  
## <a name="remarks"></a>备注  
 新的记录包含 VALUES 子句中列出的数据。  
  
## <a name="driver-remarks"></a>驱动程序备注  
 当你的应用程序将发送到数据源的 ODBC SQL 语句插入时，Visual FoxPro ODBC 驱动程序将不转换 Visual FoxProINSERT 命令转换为命令。  
  
## <a name="see-also"></a>请参阅  
 [CREATE TABLE-SQL 命令](../../odbc/microsoft/create-table-sql-command.md)   
 [SELECT - SQL 命令](../../odbc/microsoft/select-sql-command.md)
