---
title: "行状态数组 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- row status array [ODBC]
- cursors [ODBC], block
- result sets [ODBC], row status array
- block cursors [ODBC]
- result sets [ODBC], block cursors
- rowset status [ODBC]
ms.assetid: 4b69f189-2722-4314-8a02-f4ffecd6dabd
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f4451ccb74ca19a02c352c2e7361d0ec8e84c87d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="row-status-array"></a>行状态数组
除了数据之外， **SQLFetch**和**SQLFetchScroll**可以返回一个数组，在行集中的每个行的状态。 此数组是通过的 SQL_ATTR_ROW_STATUS_PTR 语句属性指定。 此数组由应用程序分配的和必须都由 SQL_ATTR_ROW_ARRAY_SIZE 语句特性指定的所有元素。 数组中的值设置**SQLBulkOperations**， **SQLFetch**， **SQLFetchScroll**，和**SQLSetPos。** 值描述的行和自上次提取后是否该状态已更改的状态。  
  
|行状态数组值|Description|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|行提取了成功，并且自上次提取后已不更改。|  
|SQL_ROW_SUCCESS_WITH_INFO|行提取了成功，并且自上次提取后已不更改。 但是，有关行返回一条警告。|  
|SQL_ROW_ERROR|提取行时出错。|  
|SQL_ROW_UPDATED|行已成功提取和自从上次提取已更新。 如果再次提取或刷新由行**SQLSetPos**，其状态更改为新的状态。<br /><br /> 某些驱动程序无法检测到对数据的更改，因此无法返回此值。 若要确定驱动程序是否可以检测到对 refetched 行的更新，应用程序调用**SQLGetInfo** SQL_ROW_UPDATES 选项。|  
|SQL_ROW_DELETED|已删除行，因为上次提取。|  
|SQL_ROW_ADDED|插入行时发生**SQLBulkOperations**。 如果该行被再次提取，或通过刷新**SQLSetPos**，其状态为 SQL_ROW_SUCCESS。<br /><br /> 未设置此值**SQLFetch**或**SQLFetchScroll**。|  
|SQL_ROW_NOROW|行集占用该结果集的末尾，并且会不返回任何行，对应于此元素的行状态数组。|
