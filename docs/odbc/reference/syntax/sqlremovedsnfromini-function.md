---
title: SQLRemoveDSNFromIni 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveDSNFromIni
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDSNFromIni
helpviewer_keywords:
- SQLRemoveDSNFromIni function [ODBC]
ms.assetid: bb2e8273-7b61-4113-bfc8-f7ccc607c811
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4cc83a8cafffc9b5d1166df76d91ce4c63f0b858
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68024529"
---
# <a name="sqlremovedsnfromini-function"></a>SQLRemoveDSNFromIni 函数
**度**  
 引入的版本： ODBC 1。0  
  
 **总结**  
 **SQLRemoveDSNFromIni**从系统信息中删除数据源。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL SQLRemoveDSNFromIni(  
     LPCSTR   lpszDSN);  
```  
  
## <a name="arguments"></a>参数  
 *lpszDSN*  
 送要删除的数据源的名称。  
  
## <a name="returns"></a>返回  
 如果该函数删除了数据源或该数据源不在 Odbc .ini 文件中，则该函数返回 TRUE。 如果无法删除数据源，则返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLRemoveDSNFromIni**返回 FALSE 时，可以* \** 通过调用**SQLInstallerError**获取关联的 pfErrorCode 值。 下表列出了可由**SQLInstallerError**返回的* \*pfErrorCode*值，并说明了此函数的上下文中的每个值。  
  
|*\*pfErrorCode*|错误|说明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|出现错误，但没有特定的安装程序错误。|  
|ODBC_ERROR_INVALID_DSN|DSN 无效|*LpszDSN*参数无效。|  
|ODBC_ERROR_REQUEST_FAILED|请求失败|安装程序无法从注册表中删除 DSN 信息。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行此功能。|  
  
## <a name="comments"></a>注释  
 **SQLRemoveDSNFromIni**从系统信息的 [ODBC 数据源] 部分删除数据源名称。 它还将从系统信息中删除数据源规范部分。  
  
 只应从驱动程序安装程序库中调用此函数。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|请参阅|  
|---------------------------|---------|  
|添加、修改或删除数据源|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|添加、修改或删除数据源|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|删除默认数据源|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|向系统信息中添加数据源名称|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
