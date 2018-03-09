---
title: "SET 路径命令 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SET PATH command [ODBC]
ms.assetid: db488d1e-0963-4f45-8c76-a23b9bde9e9d
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 553c3f464b5a14d578aa05bece939126f7251974
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="set-path-command"></a>SET 路径命令
指定文件搜索的路径。 特定于驱动程序的信息，请参阅备注。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET PATH TO [Path]  
```  
  
## <a name="arguments"></a>参数  
 到 [*路径*]  
 指定您希望 Visual FoxPro 要搜索的目录。 使用逗号或分号分隔到单独的目录。  
  
## <a name="remarks"></a>Remarks  
 设置路径，可指定可以在存储过程中调用其他 Visual FoxPro 程序用于搜索路径。 设置路径不会更改你为连接指定的数据源的路径。  
  
 将路径设置为而无需发出*路径*要还原到默认目录或文件夹的路径。  
  
## <a name="driver-remarks"></a>驱动程序备注  
 如果在存储过程发出设置路径，它将通过使用以下函数和命令被忽略：  
  
-   目录函数如[SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)和[SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)将忽略新路径，并继续引用的数据源中指定的路径[SQLPrepare](../../odbc/microsoft/sqlprepare-visual-foxpro-odbc-driver.md)或[SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)。  
  
-   如选择、 插入、 更新、 删除和 CREATE TABLE 命令将忽略新路径和继续引用的数据源中指定的路径**SQLPrepare**或**SQLExecDirect**。  
  
 如果你在存储过程颁发设置路径，并不随后将路径设置回其原始状态，与数据库的其他连接将使用新路径，（因为到数据的会话不作用域设置路径）。  
  
 如果你想要创建、 选择，或更新之外，数据源所指定的目录中的表，请与你的命令指定文件的完整路径。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC Visual FoxPro 安装程序对话框](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)   
 [SQLColumns （Visual FoxPro ODBC 驱动程序）](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)   
 [SQLDriverConnect （Visual FoxPro ODBC 驱动程序）](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)   
 [SQLTables（Visual FoxPro ODBC 驱动程序）](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)
