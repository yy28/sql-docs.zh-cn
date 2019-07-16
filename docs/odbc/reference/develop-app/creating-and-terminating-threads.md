---
title: 创建和终止线程 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- terminating threads [ODBC]
- threads [ODBC]
- multithreaded applications [ODBC]
ms.assetid: a2cf98ef-1c71-4742-8ee2-b53fd8e04333
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b97f29ad06c4ed961f3cee571b0ca7b8d9c0b774
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002080"
---
# <a name="creating-and-terminating-threads"></a>创建和终止线程
使用 ODBC 的多线程应用程序应调用 Microsoft® Visual C++® 运行时库函数 **_beginthread**并 **_endthread** (或 **_beginthreadex**并 **_endthreadex**) 来创建和终止线程的调用 ODBC 驱动程序管理器。 如果应用程序调用 Microsoft Windows NT® 函数**CreateThread**并**EndThread**相反，内存泄漏原因是驱动程序管理器和某些 ODBC 驱动程序调用 C 运行时将发生函数通过调用创建的线程上不起**CreateThread**。 有关详细信息，请参阅 Microsoft Windows® 文档。
