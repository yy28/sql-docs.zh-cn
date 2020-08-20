---
description: 创建和终止线程
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
ms.openlocfilehash: c0100b85bc596149d809dee7e6c4cb3547dbd081
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465849"
---
# <a name="creating-and-terminating-threads"></a>创建和终止线程
使用 ODBC 的多线程应用程序®应 Visual C++®运行时库函数 **_beginthread**并 **_endthread** (_beginthreadex 或 **_endthreadex**) **_endthreadex** 如果应用程序调用 Microsoft Windows NT®函数 **CreateThread** 和 **EndThread** ，则会发生内存泄漏，因为驱动程序管理器和某些 ODBC 驱动程序调用 C 运行时函数，这些函数将无法在通过调用 **CreateThread**创建的线程上运行。 有关详细信息，请参阅 Microsoft Windows®文档。
