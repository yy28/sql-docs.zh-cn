---
title: 插入 - SQL 命令 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ce00005fb1aa0ca9732fc5e9cfeacd6faf6ef9e1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299999"
---
# <a name="insert---sql-command"></a>INSERT - SQL 命令
将记录追加到包含指定字段值的表的末尾。  
  
 Visual FoxPro ODBC 驱动程序支持此命令的本机 Visual FoxPro 语言语法。 有关特定于驱动程序的信息，请参阅备注。  
  
## <a name="syntax"></a>语法  
  
```  
  
INSERT INTO dbf_name [(fname1 [, fname2, ...])]  
   VALUES (eExpression1 [, eExpression2, ...])  
```  
  
## <a name="arguments"></a>参数  
 插入*到dbf_name*  
 指定追加新记录的表的名称。 *dbf_name*可以包含路径，也可以是名称表达式。  
  
 如果指定的表未打开，则它将在新工作区中专门打开，并将新记录追加到表中。 未选择新工作区;未选择新工作区。当前工作区保持选中状态。  
  
 如果指定的表处于打开状态，则 INSERT 将新记录追加到表中。 如果表在当前工作区以外的工作区中打开，则在追加记录后不会选择该表;如果表在当前工作区以外的工作区域中打开，则不会选择该表。当前工作区保持选中状态。  
  
 *[（fname1*[， *fname2*[， .]） ]  
 在新记录中指定插入值的字段的名称。  
  
 值 *（eExpression1*[， *eExpression2*]， .*）  
 指定插入到新记录中的字段值。 如果省略字段名称，则必须按表结构定义的顺序指定字段值。  
  
## <a name="remarks"></a>备注  
 新记录包含 VALUE 子句中列出的数据。  
  
## <a name="driver-remarks"></a>驱动程序备注  
 当应用程序将 ODBC SQL 语句 INSERT 发送到数据源时，Visual FoxPro ODBC 驱动程序将该命令转换为 Visual FoxProINSERT 命令，无需翻译。  
  
## <a name="see-also"></a>另请参阅  
 [创建表 - SQL 命令](../../odbc/microsoft/create-table-sql-command.md)   
 [SELECT - SQL 命令](../../odbc/microsoft/select-sql-command.md)
