---
title: 插入的 SQL 命令 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- INSERT [ODBC]
ms.assetid: 9b648198-349f-46f6-b869-13d129945971
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 881ee4d74eab6b1e26b1f3ec243a39c08125ea00
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="insert---sql-command"></a>插入的 SQL 命令
到包含的指定的字段值的表的末尾追加一条记录。  
  
 Visual FoxPro ODBC 驱动程序支持本机 Visual FoxPro 语言语法，此命令。 特定于驱动程序的信息，请参阅备注。  
  
## <a name="syntax"></a>语法  
  
```  
  
INSERT INTO dbf_name [(fname1 [, fname2, ...])]  
   VALUES (eExpression1 [, eExpression2, ...])  
```  
  
## <a name="arguments"></a>参数  
 INSERT INTO *dbf_name*  
 指定新的记录追加到表的名称。 *dbf_name*可以包括了路径和可以是的名称表达式。  
  
 如果您指定的表未打开，它将以独占方式在新的工作区中打开和新的记录追加到表。 未选择新的工作区域;当前工作区保持选定状态。  
  
 如果您指定的表已打开，插入到表追加新的记录。 如果表是在工作区中打开的而非当前工作区，它不选择追加记录; 后当前工作区保持选定状态。  
  
 [( *fname1*[， *fname2*[，...]])]  
 指定新记录中的字段的名称值将插入到。  
  
 值 ( *eExpression1*[， *eExpression2*[，...]])  
 指定插入新记录的字段值。 如果省略字段名称，必须由表结构定义的顺序来指定字段值。  
  
## <a name="remarks"></a>注释  
 新的记录包含 VALUES 子句中列出的数据。  
  
## <a name="driver-remarks"></a>驱动程序备注  
 当你的应用程序将 ODBC SQL 语句 INSERT 发送到数据源时，Visual FoxPro ODBC 驱动程序将不转换 Visual FoxProINSERT 命令转换为命令。  
  
## <a name="see-also"></a>另请参阅  
 [创建表的 SQL 命令](../../odbc/microsoft/create-table-sql-command.md)   
 [SELECT - SQL 命令](../../odbc/microsoft/select-sql-command.md)
