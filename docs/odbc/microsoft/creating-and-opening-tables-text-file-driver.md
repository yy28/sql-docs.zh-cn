---
title: 创建和打开表（文本文件驱动程序） |Microsoft Docs
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
ms.openlocfilehash: b36c02d772682088a799cfca66f5bbf3e169a67f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096545"
---
# <a name="creating-and-opening-tables-text-file-driver"></a>创建和打开表（文本文件驱动程序）
使用文本驱动程序时，将使用 Odbcinst.ini 中指定的格式创建一个新表。 如果未指定，则以 CSVDELIMITED 格式创建表。 默认情况下，整数列默认为11个字符，而 FLOAT 列默认为22个字符。 日期列使用 YYYY-MM-DD 格式。 CHAR 和 LONGCHAR 列是 CREATE 语句中指定的宽度。
