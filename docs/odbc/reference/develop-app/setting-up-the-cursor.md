---
description: 设置游标
title: 设置游标 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: b80afb0e-ef2f-408f-86f5-a392edd99a56
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 307245dc403167f5bd857005f084ed22498d3ee8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424579"
---
# <a name="setting-up-the-cursor"></a>设置游标
应用程序可以在执行创建结果集的语句之前指定游标类型。 它通过 SQL_ATTR_CURSOR_TYPE 语句特性来执行此功能。 如果应用程序未显式指定类型，则将使用只进游标。 若要获取混合游标，应用程序需要指定由键集驱动的游标，但声明的键集大小小于结果集的大小。  
  
 对于键集驱动游标和混合游标，应用程序还可以指定键集大小。 它通过 SQL_ATTR_KEYSET_SIZE 语句特性来执行此功能。 如果键集大小设置为0（默认值），则键集大小设置为结果集大小，并使用由键集驱动的游标。 在打开游标后，可以更改键集大小。  
  
 应用程序还可以设置行集大小;有关详细信息，请参阅本部分前面的 [使用块游标](../../../odbc/reference/develop-app/using-block-cursors.md)。
