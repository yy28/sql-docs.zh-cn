---
title: SQLPost安装程序错误功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLPostInstallerError
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPostInstallerError
helpviewer_keywords:
- SQLPostInstallerError function [ODBC]
ms.assetid: 4c60d827-b2d2-4f27-b220-daa9e1fcdd8d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cdceff5c4e175ba9f135c6e5e4405933b1a86b7c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306888"
---
# <a name="sqlpostinstallererror-function"></a>SQLPostInstallerError 函数
**一致性**  
 版本介绍： ODBC 3.0  
  
 **摘要**  
 **SQLPost安装程序Error**为驱动程序或转换器设置库提供了一种机制，用于向安装程序错误队列报告**配置驱动程序**、**配置DSN**和**配置器函数**的错误。 应用程序不使用此 API;因此，应用程序不会使用此 API。他们使用**SQL 安装程序错误**来检索错误。  
  
## <a name="syntax"></a>语法  
  
```cpp  
  
RETCODE SQLPostInstallerError(  
     DWORD    fErrorCode,  
     LPSTR    szErrorMsg);  
```  
  
## <a name="arguments"></a>参数  
 *fErrorCode*  
 [输入]安装程序错误代码。  
  
 *什洛姆斯格*  
 [输入]错误消息文本。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS或SQL_ERROR。  
  
## <a name="diagnostics"></a>诊断  
 **SQLPost安装程序错误**不会为自己发布错误值。 如果错误已成功发布到安装程序错误队列（使用**SQL 安装程序错误**可检索），则返回SQL_SUCCESS。 如果*dwErrorCode*参数中的值不是指定的安装程序错误代码之一，则将返回SQL_ERROR。  
  
## <a name="related-functions"></a>相关函数  
  
|有关以下方面的信息|查看|  
|---------------------------|---------|  
|添加、修改或删除驱动程序|[配置驱动程序](../../../odbc/reference/syntax/configdriver-function.md)|  
|添加、修改或删除数据源|[配置DSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|设置翻译选项|[配置转换器](../../../odbc/reference/syntax/configtranslator-function.md)|
