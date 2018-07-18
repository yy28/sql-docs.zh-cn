---
title: 出现算术错误 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
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
ms.openlocfilehash: 867de0b8982b22f9f9574c334226bccc01798065
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32899492"
---
# <a name="arithmetic-errors"></a>出现算术错误
ODBC 驱动程序计算结果中的 SELECT 语句的 WHERE 子句，因为它，则提取每个行。 如果某一行包含一个值，会导致出现算术错误，例如通过零除或数值溢出，驱动程序返回所有行，但都返回的列出现算术错误的错误。 插入或更新时，然而，ODBC 驱动程序将会停止插入或更新数据时遇到的第一个的算术错误。
