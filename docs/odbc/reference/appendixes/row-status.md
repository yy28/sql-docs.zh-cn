---
title: 行状态 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- row status [ODBC]
- cache [ODBC]
ms.assetid: 0f0b1fb6-f697-4ced-811c-2908e210bc71
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a62bad0e69a8bf8b5365575f97e4791cbbf270d6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68057108"
---
# <a name="row-status"></a>行状态
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 游标库在缓存中为行状态创建一个缓冲区。 游标库从此缓冲区检索行状态数组的值（用 SQL_ATTR_ROW_STATUS_PTR 语句特性指定）。 对于每一行，游标库将此缓冲区设置为：  
  
-   SQL_ROW_DELETED 在该行上执行定位的 delete 语句时。  
  
-   SQL_ROW_ERROR 在使用**SQLFetch**从数据源检索行时遇到错误。  
  
-   SQL_ROW_SUCCESS 成功从**SQLFetch**的数据源中提取行时。  
  
-   在行上执行定位的 update 语句时，SQL_ROW_UPDATED。
