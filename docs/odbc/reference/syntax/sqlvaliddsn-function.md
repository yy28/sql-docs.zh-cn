---
title: SQLValidDSN 函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4560f4645bf8e4e8c255b94c940b0922483cf5f6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32917722"
---
# <a name="sqlvaliddsn-function"></a>SQLValidDSN 函数
**一致性**  
 版本引入了： ODBC 2.0  
  
 **摘要**  
 **SQLValidDSN**检查长度和数据源名称的有效性之前的名称添加到的系统信息。  
  
## <a name="syntax"></a>语法  
  
```  
  
BOOL SQLValidDSN(  
     LPCSTR    lpszDSN);  
```  
  
## <a name="arguments"></a>参数  
 *lpszDSN*  
 [输入]数据源要检查的名称。  
  
## <a name="returns"></a>返回  
 如果数据源名称有效，该函数将返回 TRUE。 如果数据源名称无效或函数调用失败，则返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLValidDSN**返回 FALSE，一个关联 *\*pfErrorCode*可通过调用获取值**SQLInstallerError**。 A  *\*pfErrorCode*如果，则返回仅在函数调用失败时，不返回 FALSE，因为数据源名称无效。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError**并解释此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|对于发生了错误其中没有任何特定的安装程序错误。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该函数。|  
  
## <a name="comments"></a>注释  
 **SQLValidDSN**由驱动程序的调用[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)检查数据源名称的长度和数据源名称中的每个字符的有效性。 它会检查是否名称的长度大于 SQL_MAX_DSN_LENGTH，Sqlext.h 中定义。 (通过检查程序数据源名称的长度[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)。)**SQLValidDSN**检查是否任何下列无效字符都包含数据源名称：  
  
 [ ] { } ( ) , ; ? * = ! @ \  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|添加、 修改或删除数据源|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) （在安装程序 DLL）|  
|添加、 修改或删除数据源|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|写入到的系统信息的数据源名称|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
