---
title: 行状态数组 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304286"
---
# <a name="row-status-array"></a>行状态数组
除了数据之外 **，SQLFetch**和**SQLFetchScroll**可以返回一个数组，该数组提供行集中每行的状态。 此数组通过SQL_ATTR_ROW_STATUS_PTR语句属性指定。 此数组由应用程序分配，并且必须具有SQL_ATTR_ROW_ARRAY_SIZE语句属性指定的尽可能多的元素。 数组中的值由**SQLBulk 操作****、SQLFetch、SQLFetchScroll**和**SQLSetPos**设置。 **SQLFetchScroll** 这些值描述行的状态以及自上次提取行以来该状态是否已更改。  
  
|行状态数组值|描述|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|该行已成功提取，自上次提取以来未更改。|  
|SQL_ROW_SUCCESS_WITH_INFO|该行已成功提取，自上次提取以来未更改。 但是，返回了有关该行的警告。|  
|SQL_ROW_ERROR|提取行时出错。|  
|SQL_ROW_UPDATED|该行已成功提取，自上次提取以来已更新。 如果**SQLSetPos**再次提取或刷新该行，则其状态将更改为新状态。<br /><br /> 某些驱动程序无法检测对数据的更改，因此无法返回此值。 要确定驱动程序是否可以检测更新以重新提取行，应用程序使用SQL_ROW_UPDATES选项调用**SQLGetInfo。**|  
|SQL_ROW_DELETED|自上次提取行以来，该行已被删除。|  
|SQL_ROW_ADDED|该行由**SQLBulk 操作**插入。 如果再次提取该行或由**SQLSetPos**刷新，则其状态为SQL_ROW_SUCCESS。<br /><br /> 此值不是由**SQLFetch**或**SQLFetchScroll**设置的。|  
|SQL_ROW_NOROW|行集与结果集的末尾重叠，并且不会返回对应于行状态数组的此元素的行。|
