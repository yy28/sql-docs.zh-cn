---
title: SQL安装转换器映射 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8ab5ebccaac7ccf6374971c1d21040ad15fb3e55
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300579"
---
# <a name="sqlinstalltranslator-mapping"></a>SQLInstallTranslator 映射
当 ODBC *2.x*应用程序通过 ODBC *3.x*驱动程序调用**SQLInstall 转换器**时，驱动程序管理器将呼叫映射到**SQLInstall 翻译器Ex**。应用程序不应在 ODBC *3.x*驱动程序管理器中调用**SQLInstall 转换器***，lpszInfFile*参数设置为 NULL 以外的值。 ODBC。ODBC *2.x*中使用的 INF 文件在 ODBC *3.x*中不再受支持，即使对于向后兼容性也是如此。
