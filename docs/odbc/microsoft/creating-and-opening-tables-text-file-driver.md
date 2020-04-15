---
title: 创建和打开表（文本文件驱动程序） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], creating and opening tables
ms.assetid: e6a07dda-a665-4f5b-a8d6-9ff479700513
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae13312299f131d1957557db28bbe4db0bf7b4c7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280917"
---
# <a name="creating-and-opening-tables-text-file-driver"></a>创建和打开表（文本文件驱动程序）
使用文本驱动程序时，将使用 Odbcinst.ini 中指定的格式创建新表。 如果未指定，则以 CSVDELIMITED 格式创建表。 默认情况下，INTEGER 列默认为 11 个字符，FLOAT 列默认为 22 个字符。 日期列使用 YYYY-MM-DD 格式。 CHAR 和 LONGCHAR 列是 CREATE 语句中指定的宽度。
