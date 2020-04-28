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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 60dead23fe0051c05698e094f37ddad96b2b337d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304286"
---
# <a name="row-status-array"></a>行状态数组
除数据外， **SQLFetch**和**SQLFetchScroll**还可以返回一个数组，该数组提供行集中的每一行的状态。 此数组是通过 SQL_ATTR_ROW_STATUS_PTR 语句特性指定的。 此数组由应用程序分配，并且必须具有与 SQL_ATTR_ROW_ARRAY_SIZE 语句特性指定的数目相同的元素。 数组中的值由**SQLBulkOperations**、 **SQLFetch**、 **SQLFetchScroll**和**SQLSetPos 设置。** 值描述行的状态，以及该状态自上次提取后是否已更改。  
  
|行状态数组值|说明|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|该行已成功提取，自从上次提取后未发生更改。|  
|SQL_ROW_SUCCESS_WITH_INFO|该行已成功提取，自从上次提取后未发生更改。 但对于该行，返回了警告。|  
|SQL_ROW_ERROR|提取行时出错。|  
|SQL_ROW_UPDATED|该行已成功提取，自从上次提取后已被更新。 如果再次提取或刷新**SQLSetPos**，则其状态将更改为新状态。<br /><br /> 某些驱动程序无法检测到数据更改，因此无法返回此值。 若要确定驱动程序是否可以检测到制约行的更新，应用程序需要使用 SQL_ROW_UPDATES 选项调用**SQLGetInfo** 。|  
|SQL_ROW_DELETED|该行自上次提取之后已被删除。|  
|SQL_ROW_ADDED|该行由**SQLBulkOperations**插入。 如果再次提取行或**SQLSetPos**刷新该行，则其状态将 SQL_ROW_SUCCESS。<br /><br /> 此值不是由**SQLFetch**或**SQLFetchScroll**设置的。|  
|SQL_ROW_NOROW|行集与结果集的末尾重叠，并且未返回对应行状态数组的此元素的行。|
