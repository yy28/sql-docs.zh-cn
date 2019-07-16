---
title: SQLInstallTranslator 映射 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLInstallTranslator function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLInstallTranslator
ms.assetid: bcd9ba4f-7834-4bc4-876e-c7478998e524
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6433df796c88abd7873915266d1a2ca4041a5c62
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125730"
---
# <a name="sqlinstalltranslator-mapping"></a>SQLInstallTranslator 映射
当 ODBC *2.x*应用程序调用**SQLInstallTranslator**通过 ODBC *3.x*驱动程序，驱动程序管理器将映射到调用**SQLInstallTranslatorEx**。应用程序不应调用**SQLInstallTranslator**在 ODBC *3.x*使用的驱动程序管理器*lpszInfFile*参数设置为非 NULL 值。 ODBC。在 ODBC 中使用的 INF 文件*2.x*不再支持 ODBC *3.x*，即使为了向后兼容。
