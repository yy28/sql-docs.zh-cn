---
description: 直接连接到驱动程序
title: 直接连接到驱动程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SqlDriverConnect
- SQLDriverConnect function [ODBC], connecting directly to drivers
- connecting to driver [ODBC], drivers
ms.assetid: f86e198f-a088-4401-9106-aa62a0eb8f6e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6dbf1d7a11f0ca4d6e7d049d425451b5f0e26c2d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461519"
---
# <a name="connecting-directly-to-drivers"></a>直接连接到驱动程序
正如本部分前面所述， [选择数据源或驱动程序](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)中所述，某些应用程序根本不想使用数据源。 相反，他们需要直接连接到驱动程序。 **SQLDriverConnect** 为应用程序提供了一种无需指定数据源即可直接连接到驱动程序的方法。 从概念上讲，在运行时创建临时数据源。  
  
 若要直接连接到驱动程序，应用程序需在连接字符串中指定 **driver** 关键字，而不是 **DSN** 关键字。 **Driver**关键字的值是**SQLDrivers**返回的驱动程序的说明。 例如，假设驱动程序具有说明 Paradox 驱动程序，并且需要包含数据文件的目录的名称。 若要连接到此驱动程序，应用程序可以使用以下任一连接字符串：  
  
```  
DRIVER={Paradox Driver};Directory=C:\PARADOX;  
DRIVER={Paradox Driver};  
```  
  
 对于第一个字符串，驱动程序不需要任何其他信息。 对于第二个字符串，驱动程序需要提示输入包含数据文件的目录的名称。
