---
title: "出现算术错误 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- arithmetic errors [ODBC]
- desktop database drivers [ODBC], arithmetic errors
ms.assetid: 1c47bfac-7455-4487-b673-6b47d2a2d756
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a0a24a87c814c51bcf3270298b56b5ffec01fa29
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="arithmetic-errors"></a>出现算术错误
ODBC 驱动程序计算结果中的 SELECT 语句的 WHERE 子句，因为它，则提取每个行。 如果某一行包含一个值，会导致出现算术错误，例如通过零除或数值溢出，驱动程序返回所有行，但都返回的列出现算术错误的错误。 插入或更新时，然而，ODBC 驱动程序将会停止插入或更新数据时遇到的第一个的算术错误。
