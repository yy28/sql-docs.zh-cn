---
title: 记录计数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- record count [ODBC]
- descriptors [ODBC], record count
ms.assetid: 46eec3cc-0ecc-4980-9020-fb74a9af5730
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ca1ed60d44b1c8133c51e78a769ca6d92d9bb6b0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="record-count"></a>记录计数
描述符的 SQL_DESC_COUNT 标头字段是包含数据的最高编号记录的基于 1 的索引。 此字段不是所有列或参数绑定的计数。 如果分配的描述符，SQL_DESC_COUNT 的初始值为 0。  
  
 该驱动程序会采取任何措施分配和维护需要保存描述符信息任何存储所需。 未显式指定一个说明符的大小不未分配新记录应用程序。 在应用程序提供描述符记录其数高于 SQL_DESC_COUNT 的值的信息，该驱动程序会自动增加 SQL_DESC_COUNT。 当应用程序解除绑定的最高编号描述符记录时，该驱动程序会自动减小 SQL_DESC_COUNT 要包含的最高的剩余绑定记录数。
