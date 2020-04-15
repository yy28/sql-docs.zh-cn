---
title: 语句属性 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], statement attributes
- statement attributes [ODBC]
ms.assetid: 4c59cd8e-a713-4095-9065-20d5bdeafe43
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec24cc43e8c57e47ddda9f20fac1807f42453e84
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299640"
---
# <a name="statement-attributes"></a>语句属性
语句属性是 语句的特征。 例如，是否使用书签以及使用哪种游标与语句的结果集是语句属性。  
  
 语句属性使用**SQLSetStmtAttr**及其当前设置使用**SQLGetStmtAttr**进行设置。 没有要求应用程序设置任何语句属性;因此，应用程序可以设置任何语句属性。所有语句属性都有默认值，其中一些属性特定于驱动程序。  
  
 可以设置语句属性时，取决于属性本身。 在执行语句之前，必须设置SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE、SQL_ATTR_SIMULATE_CURSOR 和SQL_ATTR_USE_BOOKMARKS语句属性。 可以随时设置SQL_ATTR_ASYNC_ENABLE和SQL_ATTR_NOSCAN语句属性，但在再次使用语句之前不会应用。 可以随时设置SQL_ATTR_MAX_LENGTH、SQL_ATTR_MAX_ROWS和SQL_ATTR_QUERY_TIMEOUT语句属性，但在再次使用语句之前是否应用这些属性是特定于驱动程序的。 可以随时设置剩余的语句属性。  
  
> [!NOTE]  
>  通过调用**SQLSetConnectAttr**在连接级别设置语句属性的能力已在 ODBC 3 中弃用。*x*. . ODBC 3.*x*应用程序不应在连接级别设置语句属性。 ODBC 3.*x*驱动程序仅需要支持此功能，如果它们应该与 ODBC 2 配合使用。*x*应用程序。 有关详细信息，请参阅附录 G 中的[SQLSetConnectOption 映射](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md)：向后兼容性的驱动程序指南。  
>   
>  这是一个例外，SQL_ATTR_METADATA_ID和SQL_ATTR_ASYNC_ENABLE属性，它们既是连接属性，也是语句属性，可以在连接级别或语句级别设置。  
>   
>  ODBC 3 中引入的语句属性均未。*x（SQL_ATTR_METADATA_ID*除外）可以在连接级别设置。  
  
 有关详细信息，请参阅[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)函数说明。
