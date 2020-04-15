---
title: 创建和终止线程 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301688"
---
# <a name="creating-and-terminating-threads"></a>创建和终止线程
使用 ODBC 的多线程应用程序应调用 Microsoft®可视化C++®运行时库函数 **_beginthread，_endthread（** 或 **_beginthreadex**和 **_endthreadex），** 以创建和终止调用 ODBC 驱动程序管理器的线程。 **_endthread** 如果应用程序调用 Microsoft Windows NT®函数**CreateThread**和**EndThread，** 则内存泄漏将发生，因为驱动程序管理器和某些 ODBC 驱动程序调用 C 运行时函数，这些函数不适用于通过调用**CreateThread**创建的线程。 有关详细信息，请参阅 Microsoft Windows®文档。
