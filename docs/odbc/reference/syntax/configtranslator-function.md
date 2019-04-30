---
title: ConfigTranslator 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: edcffe36c0185276fae89f800e1bbcfc5bc33b33
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63232024"
---
# <a name="configtranslator-function"></a>ConfigTranslator 函数
**符合性**  
 版本引入了：ODBC 2.0  
  
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
 [输入]父窗口句柄。 如果句柄为空，该函数将不显示任何对话框。  
  
 *pvOption*  
 [输出]一个 32 位转换选项。  
  
## <a name="returns"></a>返回  
 如果成功，则返回 FALSE 出现故障时，该函数返回 TRUE。  
  
## <a name="diagnostics"></a>诊断  
 当**ConfigTranslator**返回 FALSE，关联 *\*pfErrorCode*值发布到安装程序错误缓冲区调用**SQLPostInstallerError**，可以通过调用中获得**SQLInstallerError**。 下表列出 *\*pfErrorCode*可以返回的值**SQLInstallerError** ，并解释了此函数的每个上下文中。  
  
|*\*pfErrorCode*|错误|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|窗口句柄无效|*HwndParent*参数为无效或为 NULL。|  
|ODBC_ERROR_DRIVER_SPECIFIC|特定于驱动程序或转换器错误|没有任何定义的 ODBC 安装程序错误特定于驱动程序的错误。 *SzError*调用中的参数**SQLPostInstallerError**函数应包含特定于驱动程序的错误消息。|  
|ODBC_ERROR_INVALID_OPTION|无效的转换选项|*PvOption*参数包含无效的值。|  
  
## <a name="comments"></a>注释  
 如果转换器仅支持单个翻译选项， **ConfigTranslator**返回 TRUE，并设置*pvOption*到 32 位选项。 否则，它确定要使用的默认转换选项。 **ConfigTranslator**可以显示一个对话框，使用该用户选择默认转换选项。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|获取翻译选项|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|选择转换器|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|翻译选项设置|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
