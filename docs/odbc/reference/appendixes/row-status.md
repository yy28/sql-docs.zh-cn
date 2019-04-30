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
manager: craigg
ms.openlocfilehash: 4ce45314cef92404fe14a43e033c14d6a272e1bf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63262488"
---
# <a name="row-status"></a>行状态
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 游标库创建在缓存中用于将行状态的缓冲区。 游标库从此缓冲区中检索行状态数组 （用 SQL_ATTR_ROW_STATUS_PTR 语句特性指定） 的值。 对于每一行，该游标库将此缓冲区设置为：  
  
-   SQL_ROW_DELETED 执行定位时删除的行的语句。  
  
-   遇到从数据源检索行时出错时 SQL_ROW_ERROR **SQLFetch**。  
  
-   SQL_ROW_SUCCESS 时它已成功从数据源提取的一行**SQLFetch**。  
  
-   SQL_ROW_UPDATED 执行定位的 update 语句在该行上时。
