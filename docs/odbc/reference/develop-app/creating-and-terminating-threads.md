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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3536deef604d7dbf645903e7d171a58cd9fec96a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301688"
---
# <a name="creating-and-terminating-threads"></a>创建和终止线程
使用 ODBC 的多线程应用程序应调用 Microsoft® Visual C++®运行时库函数 **_beginthread**并 **_endthread** （或 **_beginthreadex**和 **_ENDTHREADEX**）来创建和终止调用 ODBC 驱动程序管理器的线程。 如果应用程序调用 Microsoft Windows NT®函数**CreateThread**和**EndThread** ，则会发生内存泄漏，因为驱动程序管理器和某些 ODBC 驱动程序调用 C 运行时函数，这些函数将无法在通过调用**CreateThread**创建的线程上运行。 有关详细信息，请参阅 Microsoft Windows®文档。
