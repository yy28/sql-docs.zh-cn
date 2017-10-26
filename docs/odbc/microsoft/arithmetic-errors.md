---
title: "出现算术错误 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- arithmetic errors [ODBC]
- desktop database drivers [ODBC], arithmetic errors
ms.assetid: 1c47bfac-7455-4487-b673-6b47d2a2d756
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9d3585f6e1be7a3f9451231004979321202d7852
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="arithmetic-errors"></a>出现算术错误
ODBC 驱动程序计算结果中的 SELECT 语句的 WHERE 子句，因为它，则提取每个行。 如果某一行包含一个值，会导致出现算术错误，例如通过零除或数值溢出，驱动程序返回所有行，但都返回的列出现算术错误的错误。 插入或更新时，然而，ODBC 驱动程序将会停止插入或更新数据时遇到的第一个的算术错误。

