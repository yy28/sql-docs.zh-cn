---
title: 使用由键集驱动的游标的限制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], cursors
- keyset-driven cursors [ODBC]
ms.assetid: 59d86fed-387c-4719-9550-36343e74da44
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3c4910ebd2c6dd988e937f1e9d6a3281bb0e9741
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63192325"
---
# <a name="limitations-of-using-keyset-driven-cursors"></a>使用由键集驱动的游标的限制
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 您必须能够检索用于查询的表的单个 ROWID 列。 在联接、 查询或语句包含 DISTINCT、 GROUP BY、 UNION、 INTERSECT 或减号子句不能使用由键集驱动的游标。  
  
 此外，如果你的应用程序使用表别名，将无法使用由键集驱动的游标;所需的只进或静态游标类型。 使用由键集游标类型与表别名将导致以下错误:"[Microsoft] [Oracle ODBC 驱动程序] 不能使用由键集驱动的游标上联接，使用 union、 intersect 或减或只读结果集。"  
  
> [!NOTE]  
>  由于驱动程序处理发送到 Oracle 服务器的 SQL 语句的方式，Oracle 在内部将返回以下错误消息："ORA 00964： 表名称不在列表中。"
