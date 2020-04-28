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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8ab5ebccaac7ccf6374971c1d21040ad15fb3e55
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300579"
---
# <a name="sqlinstalltranslator-mapping"></a>SQLInstallTranslator 映射
当 ODBC 2.x*应用程序**通过 ODBC 1.x*驱动程序调用**SQLInstallTranslator**时，驱动程序管理器会将调用映射到**SQLInstallTranslatorEx**。应用程序不应*在 ODBC 2.X*驱动程序管理器中调用**SQLInstallTranslator** ，并将*lpszInfFile*参数设置为 NULL 以外的值。 ODBC。Odbc 2.x 中使用的 INF 文件在 ODBC *2.x 中不再受支持，**甚至是为了*向后兼容。
