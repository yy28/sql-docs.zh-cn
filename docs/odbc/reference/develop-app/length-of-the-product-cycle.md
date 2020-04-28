---
title: 产品周期的长度 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3d235146ffe1b4699f0064c5772407bcf40ae962
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306190"
---
# <a name="length-of-the-product-cycle"></a>产品周期长度
互操作性的最后问题是时间。 开发可互操作的应用程序所用的时间通常比开发 noninteroperable 要长。 原因在于，应用程序必须检查 DBMS 功能，针对不同 Dbms 执行相同的任务，而不是某些 Dbms 支持的功能，等等。  
  
 除了开发时间之外，还必须考虑产品生存期。 如果应用程序设计为使用一次，例如在从一个 DBMS 迁移到另一个 DBMS 时传输数据的应用程序，则没有必要再使其互操作。 应用程序将使用一次，并被丢弃。  
  
 如果应用程序长时间存在，则将其维护为可互操作的应用程序可能会更容易。 即使对于具有单个 DBMS 作为目标的自定义应用程序，也是如此。 这是因为可互操作的代码使用有限的数据库功能子集。 驱动程序需要保留这些功能，即使在面对基础 DBMS 的更改时也是如此。 因此，可互操作的代码可将对 DBMS 的更改的负担从应用程序开发人员转换为驱动程序开发人员。
