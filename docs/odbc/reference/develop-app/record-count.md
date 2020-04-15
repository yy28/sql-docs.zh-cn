---
title: 记录计数 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- record count [ODBC]
- descriptors [ODBC], record count
ms.assetid: 46eec3cc-0ecc-4980-9020-fb74a9af5730
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 28e503ae4602d87fc9138ed018ee1e95f135ec57
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281813"
---
# <a name="record-count"></a>记录计数
描述符的SQL_DESC_COUNT标头字段是包含数据的最高编号记录的基于一个索引。 此字段不是绑定的所有列或参数的计数。 分配描述符时，SQL_DESC_COUNT的初始值为 0。  
  
 驱动程序执行任何必要的操作来分配和维护它保存描述符信息所需的任何存储。 应用程序不显式指定描述符的大小，也不会分配新记录。 当应用程序为数字高于SQL_DESC_COUNT值的描述符记录提供信息时，驱动程序会自动增加SQL_DESC_COUNT。 当应用程序取消绑定编号最高的描述符记录时，驱动程序会自动减少SQL_DESC_COUNT以包含剩余绑定记录的最高数。
