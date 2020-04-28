---
title: CString 类 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CString class [ODBC]
ms.assetid: 18630642-76fa-43c4-a154-3f0969ec9b50
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0f941061bf1bc7671d4744d309770fc92c95dd6e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301646"
---
# <a name="cstring-class"></a>CString 类
由于 Microsoft®中**CString**类的对象 Visual C++®具有符号，而 odbc 函数中的字符串参数是无符号的，因此，在不强制转换的情况下，将**CString**对象传递到 odbc 函数的应用程序将收到编译器警告。
