---
description: INSERT - SQL 命令
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 92c4b2068149164716d52fd3693e56164ab788ab
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449499"
---
# <a name="insert---sql-command"></a>INSERT - SQL 命令
向包含指定字段值的表的末尾追加一条记录。  
  
 Visual FoxPro ODBC 驱动程序支持此命令的本机 Visual FoxPro 语言语法。 有关特定于驱动程序的信息，请参阅 "备注"。  
  
## <a name="syntax"></a>语法  
  
```  
  
INSERT INTO dbf_name [(fname1 [, fname2, ...])]  
   VALUES (eExpression1 [, eExpression2, ...])  
```  
  
## <a name="arguments"></a>参数  
 插入 *dbf_name*  
 指定新记录附加到的表的名称。 *dbf_name* 可以包含一个路径，并且可以是一个名称表达式。  
  
 如果您指定的表未打开，则它将以独占方式在新的工作区域中打开，而新记录将追加到该表中。 未选择新的工作区;当前工作区保持选中状态。  
  
 如果指定的表为打开状态，则 INSERT 会将新记录追加到该表中。 如果表在当前工作区之外的工作区域中打开，则在追加记录后不会选择它;当前工作区保持选中状态。  
  
 [ ( *fname1*[， *fname2*[，...]]) ]  
 在新记录中指定要插入值的字段的名称。  
  
 值 ( *eExpression1*[， *eExpression2*[，...]])   
 指定插入到新记录中的字段值。 如果省略字段名称，则必须按表结构定义的顺序指定字段值。  
  
## <a name="remarks"></a>备注  
 新记录包含 VALUES 子句中所列的数据。  
  
## <a name="driver-remarks"></a>驱动程序备注  
 当应用程序将 ODBC SQL 语句插入发送到数据源时，Visual FoxPro ODBC 驱动程序会在不进行转换的情况下将命令转换为 Visual FoxProINSERT 命令。  
  
## <a name="see-also"></a>另请参阅  
 [CREATE TABLE-SQL 命令](../../odbc/microsoft/create-table-sql-command.md)   
 [SELECT - SQL 命令](../../odbc/microsoft/select-sql-command.md)
