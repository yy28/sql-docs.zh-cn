---
title: SQLInstallTranslator 映射 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLInstallTranslator function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLInstallTranslator
ms.assetid: bcd9ba4f-7834-4bc4-876e-c7478998e524
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5de97b141f7ea2d1e3acf828f7d1b25bd77e0de7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32906892"
---
# <a name="sqlinstalltranslator-mapping"></a>SQLInstallTranslator 映射
当一个 ODBC 2。*x*应用程序调用**SQLInstallTranslator**到 ODBC 3 *.x*驱动程序，驱动程序管理器映射到调用**SQLInstallTranslatorEx**.应用程序不应调用**SQLInstallTranslator** ODBC 3 中 *.x*驱动程序管理器与*lpszInfFile*参数设置为非 NULL 值。 ODBC。ODBC 2 中使用的 INF 文件。*x* ODBC 3 中不再支持 *.x*、 甚至为了向后兼容。
