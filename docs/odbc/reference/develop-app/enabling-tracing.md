---
title: 启用跟踪 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- tracing options [ODBC], enabling
ms.assetid: 48e318bd-2487-4708-a698-ea01f36a45e9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 80bd4023a0260b67d11d7b4ded1bb810b81e0ab2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287347"
---
# <a name="enabling-tracing"></a>启用跟踪
可通过以下三种方式启用跟踪：  
  
-   在 Odbc.ini 注册表条目中设置**跟踪**和**跟踪文件**关键字。 当调用具有*SQL_HANDLE_ENV的* **SQLAllocHandle**时，这将启用或禁用跟踪。 这些选项设置在数据源设置期间显示的 ODBC 数据源管理员对话框的"跟踪"选项卡中。 有关详细信息，请参阅[数据源的注册表项](../../../odbc/reference/install/registry-entries-for-data-sources.md)。  
  
-   调用**SQLSetConnectAttr**将SQL_ATTR_TRACE连接属性设置为SQL_OPT_TRACE_ON。 这将启用或禁用连接持续时间的跟踪。 有关详细信息，请参阅[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)函数说明。  
  
-   使用**ODBC 共享跟踪Flag**动态打开或关闭跟踪。 （有关详细信息，请参阅下一个主题["动态跟踪](../../../odbc/reference/develop-app/dynamic-tracing.md)"。）
