---
title: CREATE INDEX Statement | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX [ODBC]
- SQL grammar [ODBC], create index
ms.assetid: 69438247-eef3-44c5-bef2-acef4e146f41
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 93ddc3881796aee3194ec5268afc68ecbab1a487
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63233010"
---
# <a name="create-index-statement"></a>CREATE INDEX 语句
CREATE INDEX 语句的语法是：  
  
 创建 [UNIQUE] 索引*索引名称*ON *l e-n* (*列标识符*[ASC] [DESC] [，*列标识符*[ASC][DESC]...])与\<*索引选项列表*>  
  
 其中\<*索引的选项列表*> 可以是：PRIMARY &#124; DISALLOW NULL &#124; IGNORE NULL  
  
 只有 Microsoft Access 驱动程序使用不允许 NULL 和 NULL 忽略索引选项。 DBASE 和 Paradox 驱动程序接受的语法，但忽略任一选项存在。  
  
 当使用 Paradox 驱动程序时，CREATE INDEX 语句创建 Paradox 主要密钥文件和辅助文件。  
  
 此语句不受 Microsoft Excel 或文本文件驱动程序。
