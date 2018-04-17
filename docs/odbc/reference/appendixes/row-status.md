---
title: 行状态 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
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
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3af34355fe5f2e41401643161805117612ab0614
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="row-status"></a>行状态
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 游标库创建在缓存中的行状态的缓冲区。 游标库从此缓冲区中检索行状态数组 （SQL_ATTR_ROW_STATUS_PTR 语句属性指定） 的值。 对于每一行，光标库将此缓冲区设置为：  
  
-   SQL_ROW_DELETED 执行定位时删除在该行上的语句。  
  
-   SQL_ROW_ERROR 遇到从数据源中检索行时出错时**SQLFetch**。  
  
-   SQL_ROW_SUCCESS 时它成功，则提取行从数据源**SQLFetch**。  
  
-   当它在该行上执行的定位的更新语句 SQL_ROW_UPDATED。
