---
title: 删除语句限制 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DELETE statement limitations [ODBC]
- ODBC SQL grammar, DELETE statement limitations
ms.assetid: 084761fe-e65b-4f38-ba4f-69884b2a7700
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 365b54ab8c0678253e184b397f1f71e39aed3b9b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303528"
---
# <a name="delete-statement-limitations"></a>DELETE 语句限制
Microsoft Excel 或文本驱动程序不支持 DELETE 语句。 请注意，文本驱动程序支持 INSERT 语句。  
  
 dBASE 驱动程序不支持打包表以删除"已删除"值。  
  
 要从表中删除行，表必须具有唯一索引（Paradox 主键）。
