---
title: 处理 SQL 语句的批处理 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], batches
- ODBC cursor library [ODBC], statement processing
- cursor library [ODBC], batches
- SQL statements [ODBC], cursor library
- cursor library [ODBC], statement processing
- SQL statements [ODBC], batches
- batches [ODBC], processing batches of SQL statements
ms.assetid: 04b93ef9-11de-47a3-8bd8-ba963c42f182
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c77d60ea3ef1412e66c8bf40937b45647e776e98
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62639564"
---
# <a name="processing-batches-of-sql-statements"></a>批处理 SQL 语句
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 游标库不支持的 SQL 语句，其中包括 SQL_ATTR_PARAMSET_SIZE 语句属性大于 1 的 SQL 语句的批处理。 如果应用程序提交一批 SQL 语句与游标库，则结果不确定。
