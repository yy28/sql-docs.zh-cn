---
title: "记录计数 |Microsoft 文档"
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
- record count [ODBC]
- descriptors [ODBC], record count
ms.assetid: 46eec3cc-0ecc-4980-9020-fb74a9af5730
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 11c30fb4abfeab58b1a6ea650bc41ce1f72524e0
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="record-count"></a>记录计数
描述符的 SQL_DESC_COUNT 标头字段是包含数据的最高编号记录的基于 1 的索引。 此字段不是所有列或参数绑定的计数。 如果分配的描述符，SQL_DESC_COUNT 的初始值为 0。  
  
 该驱动程序会采取任何措施分配和维护需要保存描述符信息任何存储所需。 未显式指定一个说明符的大小不未分配新记录应用程序。 在应用程序提供描述符记录其数高于 SQL_DESC_COUNT 的值的信息，该驱动程序会自动增加 SQL_DESC_COUNT。 当应用程序解除绑定的最高编号描述符记录时，该驱动程序会自动减小 SQL_DESC_COUNT 要包含的最高的剩余绑定记录数。
