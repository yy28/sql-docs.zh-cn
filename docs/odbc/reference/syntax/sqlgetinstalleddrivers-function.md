---
title: SQLGet 安装驱动程序功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetInstalledDrivers
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetInstalledDrivers
helpviewer_keywords:
- SQLGetInstalledDrivers function [ODBC]
ms.assetid: a1983a2e-0edf-422e-bd1b-ec5db40a34bc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 24793473bf4f25253ac11673df852d10cfb2c558
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303324"
---
# <a name="sqlgetinstalleddrivers-function"></a>SQLGetInstalledDrivers 函数
**一致性**  
 版本介绍： ODBC 1.0  
  
 **摘要**  
 **SQLGet安装驱动程序**读取系统信息的 [ODBC 驱动程序] 部分，并返回已安装驱动程序的说明列表。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL SQLGetInstalledDrivers(  
     LPSTR   lpszBuf,  
     WORD    cbBufMax,  
     WORD *  pcbBufOut);  
```  
  
## <a name="arguments"></a>参数  
 *lpszBuf*  
 [输出]已安装驱动程序的说明列表。 有关列表结构的信息，请参阅"注释"。  
  
 *cbBufMax*  
 [输入]*lpszBuf*的长度 。  
  
 *多布布夫*  
 [输出]以*lpszBuf*返回的字节总数（不包括空终止字节）。 如果可用于返回的字节数大于或等于*cbBufMax，**则 lpszBuf*中的驱动程序描述列表将截断为*cbBufMax*减去空终止字符。 *pcbBufOut*参数可以是空指针。  
  
## <a name="returns"></a>返回  
 如果成功，则函数返回 TRUE，如果失败，则返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGet 安装驱动程序**返回 FALSE 时，可以通过调用**SQL 安装程序获取**关联的*\*pfError 代码*值。 下表列出了**SQL 安装程序错误**可以返回的*\*pfErrorCode*值，并在此函数的上下文中解释了每个值。  
  
|*\*pfError代码*|错误|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|发生没有特定安装程序错误的错误。|  
|ODBC_ERROR_INVALID_BUFF_LEN|无效的缓冲区长度|*lpszBuf*参数为 NULL 或无效，或者*cbBufMax*参数小于或等于 0。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|注册表中找不到组件|安装程序在注册表中找不到 [ODBC 驱动程序] 部分。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该功能。|  
  
## <a name="comments"></a>注释  
 每个驱动程序描述都用空字节终止，整个列表用空字节终止。 （即，两个空字节标记列表的末尾。如果分配的缓冲区不够大，无法容纳整个列表，则列表将被截断，而不会出错。 如果空指针作为*lpszBuf*传入，则返回错误。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|返回驱动程序描述和属性|[SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|
