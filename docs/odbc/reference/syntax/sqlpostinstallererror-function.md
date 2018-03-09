---
title: "SQLPostInstallerError 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLPostInstallerError
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLPostInstallerError
helpviewer_keywords: SQLPostInstallerError function [ODBC]
ms.assetid: 4c60d827-b2d2-4f27-b220-daa9e1fcdd8d
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e1cc79480eb9ef38529612aecb263ee2892a128f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="sqlpostinstallererror-function"></a>SQLPostInstallerError 函数
**一致性**  
 版本引入了： ODBC 3.0  
  
 **摘要**  
 **SQLPostInstallerError**提供了驱动程序或转换器安装程序库为其报告错误的机制**ConfigDriver**， **ConfigDSN**，和**ConfigTranslator**到安装程序错误队列的函数。 应用程序不使用此 API;它们使用**SQLInstallerError**检索错误。  
  
## <a name="syntax"></a>语法  
  
```  
  
RETCODE SQLPostInstallerError(  
     DWORD    fErrorCode,  
     LPSTR    szErrorMsg);  
```  
  
## <a name="arguments"></a>参数  
 *fErrorCode*  
 [输入]安装程序错误代码。  
  
 *szErrorMsg*  
 [输入]错误消息文本。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS 或 SQL_ERROR。  
  
## <a name="diagnostics"></a>诊断  
 **SQLPostInstallerError**不会发送自己的错误值。 如果错误已成功发布到安装程序错误队列 (检索，则可以使用**SQLInstallerError**)，返回 SQL_SUCCESS。 如果将返回 SQL_ERROR 中的值*dwErrorCode*参数不是指定的安装程序错误代码之一。  
  
## <a name="related-functions"></a>相关函数  
  
|有关信息|请参阅|  
|---------------------------|---------|  
|添加、 修改或删除驱动程序|[ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)|  
|添加、 修改或删除数据源|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|设置翻译选项|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|
