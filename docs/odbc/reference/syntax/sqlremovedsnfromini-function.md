---
title: SQLRemoveDSNFromIni 函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
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
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac2128424e1b48ecc82a0d0534db9222ad6ee734
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlremovedsnfromini-function"></a>SQLRemoveDSNFromIni 函数
**一致性**  
 版本引入了： ODBC 1.0  
  
 **摘要**  
 **SQLRemoveDSNFromIni**从系统信息中删除数据源。  
  
## <a name="syntax"></a>语法  
  
```  
  
BOOL SQLRemoveDSNFromIni(  
     LPCSTR   lpszDSN);  
```  
  
## <a name="arguments"></a>参数  
 *lpszDSN*  
 [输入]要删除的数据源的名称。  
  
## <a name="returns"></a>返回  
 如果它会删除数据源或数据源未处于 Odbc.ini 文件，该函数返回 TRUE。 如果它无法删除数据源，则返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLRemoveDSNFromIni**返回 FALSE，一个关联 *\*pfErrorCode*可通过调用获取值**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError**并解释此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|对于发生了错误其中没有任何特定的安装程序错误。|  
|ODBC_ERROR_INVALID_DSN|无效的 DSN|*LpszDSN*自变量无效。|  
|ODBC_ERROR_REQUEST_FAILED|请求失败|安装程序无法从注册表中删除的 DSN 信息。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该函数。|  
  
## <a name="comments"></a>注释  
 **SQLRemoveDSNFromIni**删除的系统信息 [ODBC 数据源] 节中的数据源名称。 它还会删除数据源规范部分中的系统信息。  
  
 只能从驱动程序安装程序库，应调用此函数。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|添加、 修改或删除数据源|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|添加、 修改或删除数据源|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|删除默认数据源|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|将数据源名称添加到的系统信息|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
