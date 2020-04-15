---
title: SQLwriteSntoini 函数 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLWriteDSNToIni
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLWriteDSNToIni
helpviewer_keywords:
- SQLWriteDSNToIni [ODBC]
ms.assetid: dc7018b2-18d4-4657-96d0-086479a47474
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b8bb141c8f54c49ca3a5c6fc4bc15d434f91795c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286957"
---
# <a name="sqlwritedsntoini-function"></a>SQLWriteDSNToIni 函数
**一致性**  
 版本介绍： ODBC 1.0  
  
 **摘要**  
 **SQLWriteDSNToini**向系统信息添加了数据源。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL SQLWriteDSNToIni(  
     LPCSTR   lpszDSN,  
     LPCSTR   lpszDriver);  
```  
  
## <a name="arguments"></a>参数  
 *lpszDSN*  
 [输入]要添加的数据源的名称。  
  
 *lpszDriver*  
 [输入]向用户而不是物理驱动程序名称显示的驱动程序描述（通常是关联的 DBMS 的名称）。  
  
## <a name="returns"></a>返回  
 如果成功，则函数返回 TRUE，如果失败，则返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLWriteDSNToini**返回 FALSE 时，可以通过调用**SQL 安装程序错误**获得关联的*\*pfErrorCode*值。 下表列出了**SQL 安装程序错误**可以返回的*\*pfErrorCode*值，并在此函数的上下文中解释了每个值。  
  
|*\*pfError代码*|错误|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|发生没有特定安装程序错误的错误。|  
|ODBC_ERROR_INVALID_DSN|无效的 DSN|*lpszDSN*参数包含一个对 DSN 无效的字符串。|  
|ODBC_ERROR_INVALID_NAME|无效的驱动程序或翻译者姓名|*lpszDriver*参数无效。|  
|ODBC_ERROR_REQUEST_FAILED|申请失败。|安装程序未能在注册表中创建 DSN。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该功能。|  
  
## <a name="comments"></a>注释  
 **SQLWriteDSNToI**将数据源添加到系统信息的 [ODBC 数据源] 部分。 然后，它为数据源创建一个规范节，并添加一个关键字 （**驱动程序**）， 其值为驱动程序 DLL 的名称。 如果数据源规范部分已存在，则**SQLWriteDSNToi 会在**创建新节之前删除旧节。  
  
 此函数的调用方必须向系统信息的数据源规范部分添加任何特定于驱动程序的关键字和值。  
  
 如果数据源的名称为"默认 **"，SQLWriteDSNToi**还会在系统信息中创建默认驱动程序规范部分。  
  
 此函数应仅从设置 DLL 调用。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|添加、修改或删除数据源|[配置DSN（](../../../odbc/reference/syntax/configdsn-function.md)在安装程序 DLL 中）|  
|添加、修改或删除数据源|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|从系统信息中删除数据源名称|[SQLRemoveDSNfromini](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|
