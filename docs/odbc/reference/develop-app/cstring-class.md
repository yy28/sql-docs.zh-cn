---
title: CString 类 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- CString class [ODBC]
ms.assetid: 18630642-76fa-43c4-a154-3f0969ec9b50
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5e3d3f3719fbc16a72f692b809eb646e7bbcf24d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="cstring-class"></a>CString 类
因为对象的**CString** Microsoft® Visual C++® 中的类进行签名，并且在 ODBC 函数中的字符串自变量是无符号整数，应用程序传递**CString**到 ODBC 功能，而不必对象强制转换它们将收到编译器警告。
