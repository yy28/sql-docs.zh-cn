---
title: 算术错误 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299897"
---
# <a name="arithmetic-errors"></a>算术错误
ODBC 驱动程序在获取每行时评估 SELECT 语句中的 WHERE 子句。 如果行包含导致算术错误的值（如除以零或数字溢出），则驱动程序将返回所有行，但返回具有算术错误的列的错误。 但是，当插入或更新时，当遇到第一个算术错误时，ODBC 驱动程序将停止插入或更新数据。
