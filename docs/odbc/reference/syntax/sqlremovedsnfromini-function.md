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
manager: craigg
ms.openlocfilehash: dbd405189d17051c4f1a6f07c943f77d6a6289c4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63186015"
---
# <a name="sqlremovedsnfromini-function"></a>SQLRemoveDSNFromIni 函数
**符合性**  
 版本引入了：ODBC 1.0  
  
 **摘要**  
 **SQLRemoveDSNFromIni**删除数据源中的系统信息。  
  
## <a name="syntax"></a>语法  
  
```  
  
BOOL SQLRemoveDSNFromIni(  
     LPCSTR   lpszDSN);  
```  
  
## <a name="arguments"></a>参数  
 *lpszDSN*  
 [输入]要删除的数据源的名称。  
  
## <a name="returns"></a>返回  
 如果删除的数据源或数据源中的 Odbc.ini 文件不是，该函数返回 TRUE。 如果它无法删除数据源，它返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLRemoveDSNFromIni**返回 FALSE，关联 *\*pfErrorCode*可以通过调用获取的值**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError** ，并解释了此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|出错的其中没有特定的安装程序错误。|  
|ODBC_ERROR_INVALID_DSN|无效的 DSN|*LpszDSN*参数无效。|  
|ODBC_ERROR_REQUEST_FAILED|请求失败|安装程序无法从注册表删除 DSN 信息。|  
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
|将数据源名称添加到系统信息|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
