---
title: SQLInstallTranslator 函数 |Microsoft 文档
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
manager: craigg
ms.openlocfilehash: 92ae84714ad78e6dca3a653b85b7815188c56756
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32916792"
---
# <a name="sqlinstalltranslator-function"></a>SQLInstallTranslator 函数
**一致性**  
 版本引入了： ODBC 2.5 中，不推荐使用  
  
 **摘要**  
 在 ODBC 3.0 中， **SQLInstallTranslator**已被取代[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)。 调用**SQLInstallTranslator**将映射到**SQLInstallTranslatorEx**。 有关详细信息，请参阅**SQLInstallTranslatorEx**。  
  
 **SQLInstallTranslator**将返回 FALSE，如果在 ODBC 3 中的应用程序调用它 *.x*驱动程序管理器与*lpszInfFile*参数设置为非 NULL 值。 ODBC 2 中使用的 Odbc.inf 文件。*x* ODBC 3 中不再支持 *.x*、 甚至为了向后兼容。
