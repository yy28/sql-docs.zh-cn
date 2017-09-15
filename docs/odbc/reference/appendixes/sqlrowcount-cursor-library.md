---
title: "SQLRowCount （光标库） |Microsoft 文档"
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
- SQLRowCount function [ODBC], Cursor Library
ms.assetid: 781cf5a5-325e-4523-8633-d96d9e98277c
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9460f4f4bbc522fc421b7e40b261fe17a8410a09
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlrowcount-cursor-library"></a>SQLRowCount （光标库）
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题讨论使用**SQLRowCount**光标库中的函数。 有关常规信息**SQLRowCount**，请参阅[SQLRowCount 函数](../../../odbc/reference/syntax/sqlrowcount-function.md)。  
  
 在应用程序调用**SQLRowCount**与游标关联的语句，光标库将返回的驱动程序中检索到它的数据行数。  
  
 在应用程序调用**SQLRowCount**定位的更新或删除语句与相关的语句，光标库返回语句所影响的行数。  
  
 在应用程序调用**SQLRowCount**后**选择**语句，光标库返回 – 1。
