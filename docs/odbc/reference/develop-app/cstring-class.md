---
title: CString 类 |Microsoft 文档
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
- CString class [ODBC]
ms.assetid: 18630642-76fa-43c4-a154-3f0969ec9b50
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0ad2cd468e94aefaeb80cb9d983b6ea585c06fc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32907162"
---
# <a name="cstring-class"></a>CString 类
因为对象的**CString** Microsoft® Visual C++® 中的类进行签名，并且在 ODBC 函数中的字符串自变量是无符号整数，应用程序传递**CString**到 ODBC 功能，而不必对象强制转换它们将收到编译器警告。
