---
title: SQLGetData （光标库） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLGetData function [ODBC], Cursor Library
ms.assetid: ff40c9c0-b847-4426-a099-1bff47e6e872
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 96ffa184247c4fd7d05300952133c19127f979af
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32909908"
---
# <a name="sqlgetdata-cursor-library"></a>SQLGetData （光标库）
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题讨论使用**SQLGetData**光标库中的函数。 有关常规信息**SQLGetData**，请参阅[SQLGetData 函数](../../../odbc/reference/syntax/sqlgetdata-function.md)。  
  
 游标库实现**SQLGetData**通过先构造**选择**语句**其中**枚举每个绑定其缓存中存储的值的子句当前行中的列。 然后，执行**选择**语句来重新选择行并调用**SQLGetData**驱动程序以检索数据从数据源 （而不是缓存） 中。  
  
> [!CAUTION]  
>  **其中**子句通过游标库来标识当前行构造可能无法识别的任何行，标识不同的行，或标识多个行。 有关详细信息，请参阅[构造搜索语句](../../../odbc/reference/appendixes/constructing-searched-statements.md)。  
  
 如果 SQL_ATTR_USE_BOOKMARKS 语句属性设置为 SQL_UB_VARIABLE， **SQLGetData**可以对列 0，则返回书签数据调用。  
  
 调用**SQLGetData**受到以下限制：  
  
-   **SQLGetData**不能调用为只进游标。  
  
-   **SQLGetData**仅当满足以下条件时，才可以调用：**选择**语句生成的结果集;**选择**语句不包含联接， **联合**子句，或**GROUP BY**子句; 和使用一个别名或表达式选择列表中的任何列并未绑定与**SQLBindCol**。  
  
-   游标库的驱动程序支持只有一个活动语句，如果提取的结果集在执行之前的其余部分**选择**语句和调用**SQLGetData**。
