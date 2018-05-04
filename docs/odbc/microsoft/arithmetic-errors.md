---
title: 出现算术错误 |Microsoft 文档
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
- arithmetic errors [ODBC]
- desktop database drivers [ODBC], arithmetic errors
ms.assetid: 1c47bfac-7455-4487-b673-6b47d2a2d756
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f63a3c7dd14301fc77a2b4ec1565744ac5015d93
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="arithmetic-errors"></a>出现算术错误
ODBC 驱动程序计算结果中的 SELECT 语句的 WHERE 子句，因为它，则提取每个行。 如果某一行包含一个值，会导致出现算术错误，例如通过零除或数值溢出，驱动程序返回所有行，但都返回的列出现算术错误的错误。 插入或更新时，然而，ODBC 驱动程序将会停止插入或更新数据时遇到的第一个的算术错误。
