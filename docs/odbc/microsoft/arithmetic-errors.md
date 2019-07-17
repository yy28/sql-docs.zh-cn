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
ms.openlocfilehash: 2e0880e1746b4b65070fb28bf8d83aadec301aa4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138181"
---
# <a name="arithmetic-errors"></a>算术错误
ODBC 驱动程序评估中的 SELECT 语句的 WHERE 子句，如提取每个行。 如果行包含一个值，将导致算术错误，例如被零除或数值溢出时，驱动程序将返回所有行，但都返回列的算术错误的错误。 当插入或更新，但是，ODBC 驱动程序将停止插入或更新数据时遇到的第一个算术错误。
