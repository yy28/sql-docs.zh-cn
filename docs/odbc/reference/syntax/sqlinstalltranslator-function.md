---
title: SQLInstallTranslator 函数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: de493cc42980390fee94ca4d86efc8f5cd40646c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63242304"
---
# <a name="sqlinstalltranslator-function"></a>SQLInstallTranslator 函数
**符合性**  
 版本引入了：ODBC 2.5 中，不推荐使用  
  
 **摘要**  
 在 ODBC 3.0 **SQLInstallTranslator**已被取代[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)。 调用**SQLInstallTranslator**将映射到**SQLInstallTranslatorEx**。 有关详细信息，请参阅**SQLInstallTranslatorEx**。  
  
 **SQLInstallTranslator**将返回 FALSE，如果在 ODBC 3 中的应用程序调用它 *.x*使用的驱动程序管理器*lpszInfFile*参数设置为非 NULL 值。 ODBC 2 中使用的 Odbc.inf 文件。*x*不再支持在 ODBC 3 *.x*，即使为了向后兼容。
