---
title: 行状态数组 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- row status array [ODBC]
- cursors [ODBC], block
- result sets [ODBC], row status array
- block cursors [ODBC]
- result sets [ODBC], block cursors
- rowset status [ODBC]
ms.assetid: 4b69f189-2722-4314-8a02-f4ffecd6dabd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d2a04f5052a0b686d3669c976ec7c4bee09e52b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62468624"
---
# <a name="row-status-array"></a>行状态数组
除了数据之外， **SQLFetch**并**SQLFetchScroll**可以返回一个数组，其中提供行集中的每个行的状态。 此数组是通过将 SQL_ATTR_ROW_STATUS_PTR 语句属性指定的。 此数组分配的应用程序，并且必须由 SQL_ATTR_ROW_ARRAY_SIZE 语句属性指定的所有元素。 设置数组中的值**SQLBulkOperations**， **SQLFetch**， **SQLFetchScroll**，和**SQLSetPos。** 值描述的行和该状态是否已更改自上次提取的状态。  
  
|行状态数组值|描述|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|已成功提取行，并且自上次提取以来未发生更改。|  
|SQL_ROW_SUCCESS_WITH_INFO|已成功提取行，并且自上次提取以来未发生更改。 但是，有关行返回一条警告。|  
|SQL_ROW_ERROR|提取行时出错。|  
|SQL_ROW_UPDATED|行已成功提取和上次提取后进行了更新。 如果再次提取或刷新的行**SQLSetPos**，其状态更改为新状态。<br /><br /> 某些驱动程序无法检测到对数据的更改，因此不能返回此值。 若要确定驱动程序是否可以检测到 refetched 行的更新，应用程序调用**SQLGetInfo** SQL_ROW_UPDATES 选项。|  
|SQL_ROW_DELETED|已删除行，因为它上次提取。|  
|SQL_ROW_ADDED|通过插入行**SQLBulkOperations**。 如果再次提取或刷新的行**SQLSetPos**，其状态是 SQL_ROW_SUCCESS。<br /><br /> 不设置此值**SQLFetch**或**SQLFetchScroll**。|  
|SQL_ROW_NOROW|行集重叠的结果集的末尾并不返回任何行时，对应于此元素的行状态数组。|
