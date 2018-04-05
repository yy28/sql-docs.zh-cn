---
title: SQLInstallTranslator 函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: eeb4c73651b0d32311788ebd2149fdf6cd055b04
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="sqlinstalltranslator-function"></a>SQLInstallTranslator 函数
**一致性**  
 版本引入了： ODBC 2.5 中，不推荐使用  
  
 **摘要**  
 在 ODBC 3.0 中， **SQLInstallTranslator**已被取代[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)。 调用**SQLInstallTranslator**将映射到**SQLInstallTranslatorEx**。 有关详细信息，请参阅**SQLInstallTranslatorEx**。  
  
 **SQLInstallTranslator**将返回 FALSE，如果在 ODBC 3 中的应用程序调用它*.x*驱动程序管理器与*lpszInfFile*参数设置为非 NULL 值。 ODBC 2 中使用的 Odbc.inf 文件。*x* ODBC 3 中不再支持*.x*、 甚至为了向后兼容。
