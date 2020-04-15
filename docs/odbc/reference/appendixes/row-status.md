---
title: 行状态 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d4ae4169dc3f2a491663f4a86c564cfee5c2f4d6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305096"
---
# <a name="row-status"></a>行状态
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的光标功能。  
  
 游标库在缓存中为行状态创建缓冲区。 游标库从此缓冲区检索行状态数组的值（使用SQL_ATTR_ROW_STATUS_PTR语句属性指定）。 对于每行，游标库将此缓冲区设置为：  
  
-   SQL_ROW_DELETED在行上执行定位删除语句时。  
  
-   SQL_ROW_ERROR当遇到从**SQLFetch**从数据源检索行时出错时。  
  
-   SQL_ROW_SUCCESS，当它使用**SQLFetch**从数据源成功获取行时。  
  
-   SQL_ROW_UPDATED在行上执行定位更新语句时。
