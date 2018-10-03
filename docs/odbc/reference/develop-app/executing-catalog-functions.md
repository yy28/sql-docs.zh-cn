---
title: 执行目录函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], executing
- functions [ODBC], catalog functions
ms.assetid: c59cbda3-e214-4399-9edc-cfac86b378d7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: daf1ab2fc05b198e71b45cb02b4577eebee5c5b6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47704285"
---
# <a name="executing-catalog-functions"></a>执行目录函数
目录函数创建结果集，因为它等效于执行任何结果集 – 生成 SQL 语句。 事实上，目录函数通常是由执行预定义的 SQL 语句或调用附带的驱动程序或 DBMS 的预定义的过程实现的。 几乎所有内容都适用于创建结果集的 SQL 语句也适用于目录函数。 例如，SQL_ATTR_MAX_ROWS 语句属性限制目录函数返回的行数，就像它限制返回的行数**选择**语句。  
  
 若要执行的目录函数，应用程序只需调用该函数。  
  
 目录函数的详细信息，请参阅[目录函数](../../../odbc/reference/develop-app/catalog-functions.md)。
