---
title: SQLTransact（访问驱动程序） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLTransact
- SQLTransact function [ODBC], Access Driver
ms.assetid: 892b79c7-9e20-4d1f-bc60-d4b25694ca25
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4f88d3154925ab589a8519cb9205da03e8c3dc08
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299258"
---
# <a name="sqltransact-access-driver"></a>SQLTransact（Access 驱动程序）
> [!NOTE]  
>  本主题提供特定于访问驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 使用 Microsoft Access 驱动程序时，fType 参数在调用**SQLTransact**中支持*fType*参数SQL_COMMIT和SQL_ROLLBACK。  
  
 如果在提交过程中发生故障，可以使用 Microsoft Access 驱动程序设置中的修复数据库选项，或者通过使用**SQLConfigDataSource**函数中的REPAIR_DB关键字来修复受影响的数据库。
