---
title: SQL安装翻译功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallTranslator
helpviewer_keywords:
- SQLInstallTranslator function [ODBC]
ms.assetid: 453b21ff-3c2b-4069-8ff7-5c727f062d89
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b094aa730fff6db80b9addb63a92bee0f5f85b2a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300317"
---
# <a name="sqlinstalltranslator-function"></a>SQLInstallTranslator 函数
**一致性**  
 版本介绍： ODBC 2.5， 已弃用  
  
 **摘要**  
 在 ODBC 3.0 中 **，SQLInstall 转换器**已被[SQLInstall 翻译器所取代](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)。 对**SQLInstall 翻译器的**调用将映射到**SQLInstall 翻译器Ex**。 有关详细信息，请参阅**SQLInstall 翻译器Ex**。  
  
 如果应用程序在 ODBC *3.x*驱动程序管理器中调用它 *，lpszInfFile*参数设置为 NULL 以外的值 **，SQLInstall 转换器**将返回 FALSE。 ODBC *2.x*中使用的 Odbc.inf 文件在 ODBC *3.x*中不再受支持，即使对于向后兼容性也是如此。
