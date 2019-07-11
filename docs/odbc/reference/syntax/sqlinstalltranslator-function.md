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
ms.openlocfilehash: 08a9e3a1afef8b9ea3bf1f4266196341e0edeb76
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792865"
---
# <a name="sqlinstalltranslator-function"></a>SQLInstallTranslator 函数
**符合性**  
 版本引入了：ODBC 2.5 中，不推荐使用  
  
 **摘要**  
 在 ODBC 3.0 **SQLInstallTranslator**已被取代[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)。 调用**SQLInstallTranslator**将映射到**SQLInstallTranslatorEx**。 有关详细信息，请参阅**SQLInstallTranslatorEx**。  
  
 **SQLInstallTranslator**将返回 FALSE，如果在 ODBC 中的应用程序调用它*3.x*使用的驱动程序管理器*lpszInfFile*参数设置为非 NULL 值。 ODBC 中使用的 Odbc.inf 文件*2.x*不再支持 ODBC *3.x*，即使为了向后兼容。
