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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ab1b472540d1978a6e7a06d94da7542cc641e999
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299897"
---
# <a name="arithmetic-errors"></a>算术错误
ODBC 驱动程序会在 SELECT 语句中的 WHERE 子句提取每一行时对其进行求值。 如果某行包含的值导致算术错误（如被零除或数值溢出），则驱动程序将返回所有行，但对于出现算术错误的列返回错误。 但是，在插入或更新时，ODBC 驱动程序会在遇到第一个算术错误时停止插入或更新数据。
