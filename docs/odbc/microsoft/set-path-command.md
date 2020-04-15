---
title: 设置 PATH 命令 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET PATH command [ODBC]
ms.assetid: db488d1e-0963-4f45-8c76-a23b9bde9e9d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e44093c3ea18bc995264a8974726f5af0abe3b3a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300817"
---
# <a name="set-path-command"></a>SET PATH 命令
指定文件搜索的路径。 有关特定于驱动程序的信息，请参阅备注。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET PATH TO [Path]  
```  
  
## <a name="arguments"></a>参数  
 到 [*路径*]  
 指定您希望 Visual FoxPro 搜索的目录。 使用逗号或分号分隔目录。  
  
## <a name="remarks"></a>备注  
 SET PATH 允许您为可在存储过程中调用的其他 Visual FoxPro 程序指定搜索路径。 SET PATH 不会更改您为连接指定的数据源的路径。  
  
 发出"设置路径到无*路径*"以还原默认目录或文件夹的路径。  
  
## <a name="driver-remarks"></a>驱动程序备注  
 如果在存储过程中发出 SET PATH，则以下函数和命令将忽略它：  
  
-   目录函数（如[SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)和[SQLColumns）](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)将忽略新路径，并继续引用[SQLPrepare](../../odbc/microsoft/sqlprepare-visual-foxpro-odbc-driver.md)或[SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)中数据源指定的路径。  
  
-   选择、插入、更新、删除和创建表等命令将忽略新路径，并继续引用**SQLPrepare**或**SQLExecDirect**中数据源指定的路径。  
  
 如果在存储过程中发出 SET PATH，并且随后未将路径设置为其原始状态，则到数据库的其他连接将使用新路径（因为 SET PATH 未限定为数据会话）。  
  
 如果要在目录中创建、选择或更新数据源指定的表以外的表，请使用命令指定文件的完整路径。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC 可视化狐狸专业设置对话框](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)   
 [SQL柱（可视化福克斯Pro ODBC驱动程序）](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)   
 [SQLDriver连接（可视化福克斯Pro ODBC驱动程序）](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)   
 [SQLTables（Visual FoxPro ODBC 驱动程序）](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)
