---
title: DELETE 语句限制 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 98bd56051c724186d7308eff669263d29b82ecd5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47813825"
---
# <a name="delete-statement-limitations"></a>DELETE 语句限制
Microsoft Excel 或文本文件驱动程序不支持 DELETE 语句。 请注意文本驱动程序支持 INSERT 语句。  
  
 DBASE 驱动程序不支持将打包一个表以删除"删除"的值。  
  
 Paradox 驱动程序从表中删除一行，该表必须具有唯一索引 （Paradox 主键）。
