---
title: 视觉对象中的错误处理C++|Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- errors [ADO], Visual C++
- Visual C++ error handling [ADO]
ms.assetid: b7576f07-020a-45f7-9e79-b5756f33f7ab
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fb9eb29a78c3ec5f47e3ff09641ba04ca01d204a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925129"
---
# <a name="handling-errors-in-visual-c"></a>处理 Visual C++ 中的错误
在 COM 中，大多数操作返回一个 HRESULT 返回代码，指示函数是否已成功完成。 #Import 指令生成每个"原始"方法或属性周围的包装器代码，并检查返回的 HRESULT。 如果 HRESULT 表示失败，包装器代码将 COM 错误的 HRESULT 返回代码的调用 _com_issue_errorex() 引发作为参数。 COM 错误对象可以陷入**try catch**块。 （为提高效率的起见，捕获 _com_error 对象的引用。）  
  
 请记住，这些是 ADO 错误： 可疑 ADO 操作失败。 基础提供程序返回的错误显示为**错误**中的对象**连接**对象的**错误**集合。  
  
 #Import 指令仅创建于方法和属性在 ADO.dll 中声明的错误处理例程。 但是，您可以通过编写自己的错误检查宏或内联函数来充分利用此相同的错误处理机制。 请参阅示例的主题 Visual C++® 扩展。
