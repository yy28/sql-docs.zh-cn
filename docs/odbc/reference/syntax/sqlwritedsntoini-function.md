---
title: SQLWriteDSNToIni 函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c5a36be7a98a39cab8b9df428b8d4bd9a1d399a1
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/11/2019
ms.locfileid: "65536792"
---
# <a name="sqlwritedsntoini-function"></a>SQLWriteDSNToIni 函数
**符合性**  
 版本引入了：ODBC 1.0  
  
 **摘要**  
 **SQLWriteDSNToIni**将数据源添加到系统信息。  
  
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
 [输入]驱动程序说明 （通常关联 DBMS 的名称） 提供给用户而不是物理驱动器的名称。  
  
## <a name="returns"></a>返回  
 如果成功，则返回 FALSE 出现故障时，该函数返回 TRUE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLWriteDSNToIni**返回 FALSE，关联 *\*pfErrorCode*可以通过调用获取的值**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError** ，并解释了此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|出错的其中没有特定的安装程序错误。|  
|ODBC_ERROR_INVALID_DSN|无效的 DSN|*LpszDSN*参数包含无效的 DSN 的字符串。|  
|ODBC_ERROR_INVALID_NAME|无效的驱动程序或转换器名称|*LpszDriver*参数无效。|  
|ODBC_ERROR_REQUEST_FAILED|请求失败|安装程序无法在注册表中创建一个 DSN。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该函数。|  
  
## <a name="comments"></a>注释  
 **SQLWriteDSNToIni**将数据源添加到系统信息 [ODBC 数据源] 节。 然后创建数据源在规范部分并添加一个关键字 (**驱动程序**) 驱动程序 DLL 作为其值的名称。 如果已存在的数据源规范部分， **SQLWriteDSNToIni**创建新之前会删除旧的部分。  
  
 此函数的调用方必须将任何特定于驱动程序的关键字和值添加到数据源规范部分中的系统信息。  
  
 默认情况下，数据源的名称是否**SQLWriteDSNToIni**还会创建默认驱动程序规范部分中的系统信息。  
  
 只能从安装程序 DLL，应调用此函数。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|添加、 修改或删除数据源|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)（在安装程序 DLL）|  
|添加、 修改或删除数据源|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|从系统信息中删除数据源名称|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|
