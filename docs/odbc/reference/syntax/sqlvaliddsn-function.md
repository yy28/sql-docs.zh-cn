---
title: SQLValidDSN 函数 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLValidDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLValidDSN
helpviewer_keywords:
- SQLValidDSN [ODBC]
ms.assetid: 930d1d89-337a-4429-85a2-84ee10555ac9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6dfafca22d0b04f2147b1af24b53e787493efe67
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286967"
---
# <a name="sqlvaliddsn-function"></a>SQLValidDSN 函数
**一致性**  
 版本介绍： ODBC 2.0  
  
 **摘要**  
 **SQLValidDSN**在将名称添加到系统信息之前检查数据源名称的长度和有效性。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL SQLValidDSN(  
     LPCSTR    lpszDSN);  
```  
  
## <a name="arguments"></a>参数  
 *lpszDSN*  
 [输入]要检查的数据源名称。  
  
## <a name="returns"></a>返回  
 如果数据源名称有效，则函数将返回 TRUE。 如果数据源名称无效或函数调用失败，则返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLValidDSN**返回 FALSE 时，可以通过调用**SQL 安装程序错误**获得关联的*\*pfErrorCode*值。 仅当函数调用失败时，才返回*\*pfErrorCode，* 而不是由于数据源名称无效而返回 FALSE。 下表列出了**SQL 安装程序错误**可以返回的*\*pfErrorCode*值，并在此函数的上下文中解释了每个值。  
  
|*\*pfError代码*|错误|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|发生没有特定安装程序错误的错误。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该功能。|  
  
## <a name="comments"></a>注释  
 **SQLValidDSN**由驱动程序的[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)调用，以检查数据源名称的长度和数据源名称中各个字符的有效性。 它检查名称的长度是否大于 sqlext.h 中定义的SQL_MAX_DSN_LENGTH。 （数据源名称的长度也由[SQLWriteDSNToini 检查](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)。**SQLValidDSN**检查数据源名称中是否包含以下任何无效字符：  
  
 [ ] { } ( ) , ; ? * = ! \@ \  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|添加、修改或删除数据源|[配置DSN（](../../../odbc/reference/syntax/configdsn-function.md)在安装程序 DLL 中）|  
|添加、修改或删除数据源|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|将数据源名称写入系统信息|[SQLwriteSntoini](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
