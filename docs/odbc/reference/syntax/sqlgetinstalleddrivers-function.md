---
title: SQLGetInstalledDrivers 函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 093da37d061153013682772c3284e0afe88b7866
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47618935"
---
# <a name="sqlgetinstalleddrivers-function"></a>SQLGetInstalledDrivers 函数
**符合性**  
 版本引入了： ODBC 1.0  
  
 **摘要**  
 **SQLGetInstalledDrivers**读取系统信息 [ODBC Drivers] 部分，并返回已安装的驱动程序的说明的列表。  
  
## <a name="syntax"></a>语法  
  
```  
  
BOOL SQLGetInstalledDrivers(  
     LPSTR   lpszBuf,  
     WORD    cbBufMax,  
     WORD *  pcbBufOut);  
```  
  
## <a name="arguments"></a>参数  
 *lpszBuf*  
 [输出]安装驱动程序的说明列表。 列表结构有关的信息，请参阅"注释"。  
  
 *cbBufMax*  
 [输入]长度*lpszBuf*。  
  
 *pcbBufOut*  
 [输出]总字节数 （不包括 null 终止字节） 中返回*lpszBuf*。 可用来返回的字节数是否大于或等于*cbBufMax*，驱动程序中的说明的列表*lpszBuf*将被截断为*cbBufMax*减null 终止字符。 *PcbBufOut*参数可以是 null 指针。  
  
## <a name="returns"></a>返回  
 如果成功，则返回 FALSE 出现故障时，该函数返回 TRUE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetInstalledDrivers**返回 FALSE，关联 *\*pfErrorCode*可以通过调用获取的值**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError** ，并解释了此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|常规安装程序错误|出错的其中没有特定的安装程序错误。|  
|ODBC_ERROR_INVALID_BUFF_LEN|无效缓冲区长度|*LpszBuf*参数为 NULL 或无效，或*cbBufMax*参数为小于或等于 0。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|在注册表中找不到组件|安装程序找不到注册表中的 [ODBC Drivers] 部分。|  
|ODBC_ERROR_OUT_OF_MEM|内存不足|由于内存不足，安装程序无法执行该函数。|  
  
## <a name="comments"></a>注释  
 每个驱动程序的描述终止 null 字节，并且整个列表终止 null 字节。 （也就是说，两个 null 字节标记列表的末尾。）如果分配的缓冲区不足够大以保存整个列表，列表将被截断不会出错。 如果作为传入 null 指针，则返回错误*lpszBuf*。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|返回驱动程序说明和属性|[SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|
