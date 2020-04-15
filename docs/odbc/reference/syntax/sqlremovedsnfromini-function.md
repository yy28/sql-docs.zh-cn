---
title: SQL 删除Snfromini函数 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 848e82741954ab24941d5d519699292727ca25d6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301796"
---
# <a name="sqlremovedsnfromini-function"></a>SQLRemoveDSNFromIni 函数
**一致性**  
 版本介绍： ODBC 1.0  
  
 **摘要**  
 **SQLRemoveDSNFromIni**从系统信息中删除数据源。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL SQLRemoveDSNFromIni(  
     LPCSTR   lpszDSN);  
```  
  
## <a name="arguments"></a>参数  
 *lpszDSN*  
 [输入]要删除的数据源的名称。  
  
## <a name="returns"></a>返回  
 如果函数删除数据源或数据源不在 Odbc.ini 文件中，则该函数将返回 TRUE。 如果无法删除数据源，它将返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLRemoveDSNFromini**返回 FALSE 时，可以通过调用**SQL 安装程序错误**获得关联的*\*pfErrorCode*值。 下表列出了**SQL 安装程序错误**可以返回的*\*pfErrorCode*值，并在此函数的上下文中解释了每个值。  
  
|*\*pfError代码*|错误|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|发生没有特定安装程序错误的错误。|  
|ODBC_ERROR_INVALID_DSN|无效的 DSN|*lpszDSN*参数无效。|  
|ODBC_ERROR_REQUEST_FAILED|申请失败。|安装程序无法从注册表中删除 DSN 信息。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该功能。|  
  
## <a name="comments"></a>注释  
 **SQLRemoveDSNFromIni**从系统信息的 [ODBC 数据源] 部分中删除数据源名称。 它还从系统信息中删除数据源规范部分。  
  
 应仅从驱动程序设置库调用此功能。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|添加、修改或删除数据源|[配置DSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|添加、修改或删除数据源|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|删除默认数据源|[SQL 删除默认数据源](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|向系统信息添加数据源名称|[SQLwriteSntoini](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
