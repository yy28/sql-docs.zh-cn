---
title: 配置翻译功能 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fb2f26f87854d74a217885010014633963472787
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306028"
---
# <a name="configtranslator-function"></a>ConfigTranslator 函数
**一致性**  
 版本介绍： ODBC 2.0  
  
 **摘要**  
 **配置转换器**返回翻译器的默认翻译选项。 它可以在转换器 DLL 或单独的设置 DLL 中。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
BOOL ConfigTranslator(  
     HWND     hwndParent,  
     DWORD *  pvOption);  
```  
  
## <a name="arguments"></a>参数  
 *hwnd 家长*  
 [输入]父窗口句柄。 如果句柄为空，则函数将不会显示任何对话框。  
  
 *pvOption*  
 [输出]32 位转换选项。  
  
## <a name="returns"></a>返回  
 如果成功，则函数返回 TRUE，如果失败，则返回 FALSE。  
  
## <a name="diagnostics"></a>诊断  
 当**配置转换器**返回 FALSE 时，通过调用**SQLPost 安装程序错误**将关联的*\*pfError 代码*值发布到安装程序错误缓冲区，并且可以通过调用**SQL 安装程序错误**获得。 下表列出了**SQL 安装程序错误**可以返回的*\*pfErrorCode*值，并在此函数的上下文中解释了每个值。  
  
|*\*pfError代码*|错误|描述|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|无效的窗口句柄|*hwnd 父参数*无效或 NULL。|  
|ODBC_ERROR_DRIVER_SPECIFIC|驱动程序或转换器特定错误|驱动程序特定的错误，没有定义的 ODBC 安装程序错误。 调用**SQLPost 安装程序错误**函数时 *，SzError*参数应包含特定于驱动程序的错误消息。|  
|ODBC_ERROR_INVALID_OPTION|无效翻译选项|*pvOption*参数包含无效值。|  
  
## <a name="comments"></a>注释  
 如果转换器仅支持单个平移选项，**则配置转换器**将返回 TRUE 并将*pvOption*设置到 32 位选项。 否则，它确定要使用的默认转换选项。 **配置翻译器**可以显示一个对话框，用户可以选择默认翻译选项。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|获取翻译选项|[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|选择译员|[SQLGet 转换器](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|设置翻译选项|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|
