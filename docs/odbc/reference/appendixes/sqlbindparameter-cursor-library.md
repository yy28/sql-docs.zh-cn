---
title: SQLBind参数（光标库） |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 55708cc5192fb40149d6db7710f6ee638c4880d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305425"
---
# <a name="sqlbindparameter-cursor-library"></a>SQLBindParameter（游标库）
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的光标功能。  
  
 本主题讨论在游标库中使用**SQLBind参数**函数。 有关**SQLBind参数的**一般信息，请参阅[SQLBind参数函数](../../../odbc/reference/syntax/sqlbindparameter-function.md)。  
  
 只要绑定列的 C 数据类型、列大小和十进制数字保持不变，应用程序就可以调用**SQLBindParameter**重新绑定参数。  
  
 游标库支持将SQL_ATTR_ROW_BIND_OFFSET_PTR语句属性设置为使用绑定偏移量。 **（SQLBind 参数**不必调用，此重新绑定发生。  
  
 游标库支持绑定执行时的数据参数。
