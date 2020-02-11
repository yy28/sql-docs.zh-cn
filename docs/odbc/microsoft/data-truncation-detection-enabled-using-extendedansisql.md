---
title: 使用 ExtendedAnsiSQL 启用数据截断检测 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- truncating data [ODBC]
- extendedANSISQL [ODBC], data truncation detection
ms.assetid: cec2359b-917d-4e1d-9625-5cd678b62f10
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d7fb67171a796755bf8d6229b9d562f69bd588ed
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096512"
---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>使用 ExtendedAnsiSQL 启用的数据截断检测
当 ExtendedAnsiSQL 标志打开并且应用程序将数据插入到 char 或 binary 列中并且数据被截断时，将检测到截断。 当 ExtendedAnsiSQL 标志关闭时，数据将被截断，而不会出现警告，因为它在以前版本的 ODBC 桌面数据库驱动程序中。
