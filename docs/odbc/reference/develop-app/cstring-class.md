---
title: "CString 类 |Microsoft 文档"
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
- CString class [ODBC]
ms.assetid: 18630642-76fa-43c4-a154-3f0969ec9b50
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 723d95f4ba83ec4ffe207461256d31242f5a05ea
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="cstring-class"></a>CString 类
因为对象的**CString** Microsoft® Visual C++® 中的类进行签名，并且在 ODBC 函数中的字符串自变量是无符号整数，应用程序传递**CString**到 ODBC 功能，而不必对象强制转换它们将收到编译器警告。
