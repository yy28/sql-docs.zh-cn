---
title: "创建和终止线程 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- terminating threads [ODBC]
- threads [ODBC]
- multithreaded applications [ODBC]
ms.assetid: a2cf98ef-1c71-4742-8ee2-b53fd8e04333
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7a30fbe976ac3de550f8067cca82732631f698ac
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="creating-and-terminating-threads"></a>创建和终止线程
使用 ODBC 的多线程应用程序应调用 Microsoft® Visual C++® 运行时库函数**_beginthread**和**_endthread** (或**_beginthreadex**和**_endthreadex**) 来创建和终止调用 ODBC 驱动程序管理器的线程。 如果应用程序调用 Microsoft Windows NT® 函数**CreateThread**和**EndThread**相反，内存泄漏，会发生因为驱动程序管理器和某些 ODBC 驱动程序调用 C 运行时函数通过调用创建的线程上将无法工作**CreateThread**。 有关详细信息，请参阅 Microsoft Windows® 文档。

