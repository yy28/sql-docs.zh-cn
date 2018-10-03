---
title: SQLBindParameter （游标库） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBindParameter function [ODBC], Cursor Library
ms.assetid: 04c53e4c-cd1d-40b2-9997-684ebe43499f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eafab0f29cb4e1b7ecdfea378f9315ba29cf133f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47813665"
---
# <a name="sqlbindparameter-cursor-library"></a>SQLBindParameter（游标库）
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题介绍如何使用**SQLBindParameter**游标库中的函数。 有关常规信息**SQLBindParameter**，请参阅[SQLBindParameter 函数](../../../odbc/reference/syntax/sqlbindparameter-function.md)。  
  
 应用程序可以调用**SQLBindParameter**重新绑定参数，只要 C 数据类型、 列大小和十进制数字的绑定列保持不变。  
  
 游标库支持设置 SQL_ATTR_ROW_BIND_OFFSET_PTR 语句属性来使用绑定偏移量。 (**SQLBindParameter**无需进行此重新绑定为其调用。)  
  
 游标库支持绑定执行时数据参数。
