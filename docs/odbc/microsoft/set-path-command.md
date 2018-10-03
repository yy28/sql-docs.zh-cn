---
title: SET PATH 命令 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f3d810e66249779b2d3706e92ea39f89a0f87cff
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47727545"
---
# <a name="set-path-command"></a>SET PATH 命令
指定文件搜索的路径。 特定于驱动程序的信息，请参阅备注。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET PATH TO [Path]  
```  
  
## <a name="arguments"></a>参数  
 为 [*路径*]  
 指定您希望 Visual FoxPro 要搜索的目录。 使用逗号或分号来分隔路径。  
  
## <a name="remarks"></a>备注  
 设置路径，可指定其他 Visual FoxPro 程序可以调用存储过程中的搜索路径。 设置路径不会更改已为连接指定的数据源的路径。  
  
 将路径设置为无需发出*路径*还原到默认目录或文件夹的路径。  
  
## <a name="driver-remarks"></a>驱动程序备注  
 如果在存储过程中发出 SET PATH，它将被忽略的以下函数和命令：  
  
-   目录函数，如[SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)并[SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)将忽略新路径并将继续引用的数据源中指定的路径[SQLPrepare](../../odbc/microsoft/sqlprepare-visual-foxpro-odbc-driver.md)或[SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)。  
  
-   例如 SELECT、 INSERT、 UPDATE、 DELETE 和 CREATE TABLE 命令将忽略新路径并将继续引用的数据源中指定的路径**SQLPrepare**或**SQLExecDirect**。  
  
 如果在存储过程中发出 SET PATH，随后不将路径设置回其原始状态，其他与数据库的连接将使用新路径 （因为设置路径不限于数据会话）。  
  
 如果你想要创建、 选择，或更新之外的数据源所指定的目录中的表，指定与您的命令文件的完整路径。  
  
## <a name="see-also"></a>请参阅  
 [ODBC Visual FoxPro 设置对话框](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)   
 [SQLColumns （Visual FoxPro ODBC 驱动程序）](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)   
 [SQLDriverConnect （Visual FoxPro ODBC 驱动程序）](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)   
 [SQLTables（Visual FoxPro ODBC 驱动程序）](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)
