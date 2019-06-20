---
title: 记录计数 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8f8b0a6fc7aa5765d9373af33ab4fac0a4a07aac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63151228"
---
# <a name="record-count"></a>记录计数
描述符的 SQL_DESC_COUNT 标头字段是记录的基于 1 的编号最高包含数据的索引。 此字段不是所有列或绑定的参数的计数。 当分配的描述符时，SQL_DESC_COUNT 的初始值为 0。  
  
 驱动程序不执行任何操作所必需分配和维护保存描述符信息所需的任何存储。 应用程序不会不显式指定一个说明符的大小，也不分配新的记录。 在应用程序提供其数量高于 SQL_DESC_COUNT 的值的描述符记录的信息，该驱动程序将自动增加 SQL_DESC_COUNT。 当应用程序取消绑定编号最高的描述符记录时，该驱动程序会自动减小 SQL_DESC_COUNT 包含最高的其余绑定记录的数目。
