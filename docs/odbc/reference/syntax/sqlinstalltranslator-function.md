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
ms.openlocfilehash: e5b973332c2fe0fa541635d326a3a5adecf6ae91
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076116"
---
# <a name="sqlinstalltranslator-function"></a>SQLInstallTranslator 函数
**符合性**  
 版本引入了：ODBC 2.5 中，不推荐使用  
  
 **摘要**  
 在 ODBC 3.0 **SQLInstallTranslator**已被取代[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)。 调用**SQLInstallTranslator**将映射到**SQLInstallTranslatorEx**。 有关详细信息，请参阅**SQLInstallTranslatorEx**。  
  
 **SQLInstallTranslator**将返回 FALSE，如果在 ODBC 中的应用程序调用它*3.x*使用的驱动程序管理器*lpszInfFile*参数设置为非 NULL 值。 ODBC 中使用的 Odbc.inf 文件*2.x*不再支持 ODBC *3.x*，即使为了向后兼容。
