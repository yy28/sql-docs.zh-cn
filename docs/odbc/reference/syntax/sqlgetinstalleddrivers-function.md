---
title: "SQLGetInstalledDrivers 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLGetInstalledDrivers
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLGetInstalledDrivers
helpviewer_keywords: SQLGetInstalledDrivers function [ODBC]
ms.assetid: a1983a2e-0edf-422e-bd1b-ec5db40a34bc
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c198136c6ded3f0e9e7184a34bf3814d7e061810
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="sqlgetinstalleddrivers-function"></a>SQLGetInstalledDrivers 函数
**一致性**  
 版本引入了： ODBC 1.0  
  
 **摘要**  
 **SQLGetInstalledDrivers**读取的系统信息 [ODBC 驱动程序] 部分，并返回已安装的驱动程序的说明的列表。  
  
## <a name="syntax"></a>语法  
  
```  
  
BOOL SQLGetInstalledDrivers(  
     LPSTR   lpszBuf,  
     WORD    cbBufMax,  
     WORD *  pcbBufOut);  
```  
  
## <a name="arguments"></a>参数  
 *lpszBuf*  
 [输出]安装的驱动程序的说明列表。 有关列表结构的信息，请参阅"注释"。  
  
 *cbBufMax*  
 [输入]长度*lpszBuf*。  
  
 *pcbBufOut*  
 [输出]总字节数 （不包括 null 终止字节） 中返回*lpszBuf*。 可用于返回的字节数是否大于或等于*cbBufMax*的驱动程序中的说明列表*lpszBuf*截断为*cbBufMax*减null 终止字符。 *PcbBufOut*参数可以是 null 指针。  
  
## <a name="returns"></a>返回  
 如果它成功，则返回 FALSE 如果失败，则函数将返回 TRUE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetInstalledDrivers**返回 FALSE，一个关联 *\*pfErrorCode*可通过调用获取值**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError**并解释此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|对于发生了错误其中没有任何特定的安装程序错误。|  
|ODBC_ERROR_INVALID_BUFF_LEN|无效的缓冲区长度|*LpszBuf*参数为 NULL 或无效，或*cbBufMax*自变量为小于或等于 0。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|在注册表中找不到组件|安装程序在注册表中找不到 [ODBC 驱动程序] 部分。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该函数。|  
  
## <a name="comments"></a>注释  
 每个驱动程序说明终止与 null 字节，并且整个列表因 null 字节。 （也就是说，两个 null 字节标记列表的末尾。）如果已分配的缓冲区不大到能够容纳整个列表，列表将被截断而未出现错误。 如果作为传递 null 指针，则返回一个错误*lpszBuf*。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|返回驱动程序说明和属性|[SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|
