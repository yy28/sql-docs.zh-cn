---
title: 产品周期长度 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], product cycle
- length of the product cycle [ODBC]
ms.assetid: 4d08d886-6d8b-40fd-8544-13032f4bf6c7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c8a5b88f3fdca03be7740ba086e7ff61edbf684
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63127244"
---
# <a name="length-of-the-product-cycle"></a>产品周期长度
有关互操作性的最后一个问题是时间。 开发可互操作应用程序通常比开发一个 noninteroperable 长。 原因是应用程序必须检查 DBMS 功能、 执行相同的任务以不同的方式的不同 Dbms、 解决支持的某些 Dbms 而不是其他，功能和其他操作。  
  
 除了开发时，必须考虑产品生命周期。 如果应用程序设计为使用一次，例如当从一个 DBMS 迁移到另一个，会将数据传输的应用程序则没有必要再使其可互操作。 将使用一次应用程序，并将其丢弃。  
  
 如果应用程序将存在很长时间，它可能是更易于维护的可互操作的应用程序。 这是即使对于已作为目标的单个 DBMS 的自定义应用程序，则返回 true。 原因是可互操作的代码使用数据库功能的有限的子集。 该驱动程序需要保留提供的即使在面临对基础 DBMS 的更改时的那些功能。 因此，可互操作代码可以更改如何运用给出的负担 DBMS 将从切换到应用程序开发人员对驱动程序开发人员。
