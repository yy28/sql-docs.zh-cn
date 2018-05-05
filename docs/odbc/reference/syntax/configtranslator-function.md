---
title: ConfigTranslator 函数 |Microsoft 文档
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
- ConfigTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- ConfigTranslator
helpviewer_keywords:
- ConfigTranslator [ODBC]
ms.assetid: 7c22f07e-36de-425b-aa67-e32a84afae92
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5b38bc6340ec456ce180eb2a9cc266d5b8a19305
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="configtranslator-function"></a>ConfigTranslator 函数
**一致性**  
 版本引入了： ODBC 2.0  
  
 **摘要**  
 **ConfigTranslator**转换器将返回默认转换选项。 它可以采用转换器 DLL 或单独的安装程序 DLL。  
  
## <a name="syntax"></a>语法  
  
```  
  
BOOL ConfigTranslator(  
     HWND     hwndParent,  
     DWORD *  pvOption);  
```  
  
## <a name="arguments"></a>参数  
 *hwndParent*  
 [输入]父窗口句柄。 如果句柄为 null，函数将不显示任何对话框。  
  
 *pvOption*  
 [输出]一个 32 位转换选项。  
  
## <a name="returns"></a>返回  
 如果它成功，则返回 FALSE 如果失败，则函数将返回 TRUE。  
  
## <a name="diagnostics"></a>诊断  
 当**ConfigTranslator**返回 FALSE，一个关联 *\*pfErrorCode*值发布到安装程序错误缓冲区调用**SQLPostInstallerError**，并且可以通过调用获取**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError**并解释此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|窗口句柄无效|*HwndParent*自变量为无效或为空。|  
|ODBC_ERROR_DRIVER_SPECIFIC|特定于驱动程序或转换器错误|没有任何定义的 ODBC 安装程序错误特定于驱动程序的错误。 *SzError*对的调用中的自变量**SQLPostInstallerError**函数应包含特定于驱动程序的错误消息。|  
|ODBC_ERROR_INVALID_OPTION|无效的转换选项|*PvOption*参数包含无效值。|  
  
## <a name="comments"></a>注释  
 如果转换器支持只有单个翻译选项， **ConfigTranslator**返回 TRUE，并设置*pvOption*到 32 位选项。 否则，它确定要使用的默认转换选项。 **ConfigTranslator**可以显示对话框中与用户选择默认转换选项。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|获取转换选项|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|选择一个转换器|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|设置翻译选项|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
