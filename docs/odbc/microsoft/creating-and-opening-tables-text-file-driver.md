---
title: 创建和打开表 （文本文件驱动程序） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ce901e6a8639c8a2caea6e55cbaa18fedb56f4a7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47769095"
---
# <a name="creating-and-opening-tables-text-file-driver"></a>创建和打开表（文本文件驱动程序）
使用文本驱动程序时，使用 Odbcinst.ini 中指定的格式创建一个新表。 如果未指定，CSVDELIMITED 格式创建表。 默认情况下，整数列的默认值为 11 个字符和 FLOAT 列默认为 22 个字符。 日期列使用的年-月-日格式。 CHAR 和 LONGCHAR 列是在 CREATE 语句中指定的宽度。
