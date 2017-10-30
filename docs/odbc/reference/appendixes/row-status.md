---
title: "行状态 |Microsoft 文档"
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
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- row status [ODBC]
- cache [ODBC]
ms.assetid: 0f0b1fb6-f697-4ced-811c-2908e210bc71
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8f164b8269e1150cdf7a85e486bcc3fd93a9411f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="row-status"></a>行状态
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 游标库创建在缓存中的行状态的缓冲区。 游标库从此缓冲区中检索行状态数组 （SQL_ATTR_ROW_STATUS_PTR 语句属性指定） 的值。 对于每一行，光标库将此缓冲区设置为：  
  
-   SQL_ROW_DELETED 执行定位时删除在该行上的语句。  
  
-   SQL_ROW_ERROR 遇到从数据源中检索行时出错时**SQLFetch**。  
  
-   SQL_ROW_SUCCESS 时它成功，则提取行从数据源**SQLFetch**。  
  
-   当它在该行上执行的定位的更新语句 SQL_ROW_UPDATED。

