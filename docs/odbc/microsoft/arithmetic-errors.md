---
title: 算术错误 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arithmetic errors [ODBC]
- desktop database drivers [ODBC], arithmetic errors
ms.assetid: 1c47bfac-7455-4487-b673-6b47d2a2d756
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c0d957d6091dc5fa29ee8a0b707c0e7fe7dfc7c8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47696295"
---
# <a name="arithmetic-errors"></a>算术错误
ODBC 驱动程序评估中的 SELECT 语句的 WHERE 子句，如提取每个行。 如果行包含一个值，将导致算术错误，例如被零除或数值溢出时，驱动程序将返回所有行，但都返回列的算术错误的错误。 当插入或更新，但是，ODBC 驱动程序将停止插入或更新数据时遇到的第一个算术错误。
