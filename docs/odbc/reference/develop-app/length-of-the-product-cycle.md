---
title: 产品周期的长度 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306190"
---
# <a name="length-of-the-product-cycle"></a>产品周期长度
关于互操作性的最后一个问题是时间。 开发可互操作的应用程序通常比开发不可互操作的应用程序需要更长的时间。 原因是应用程序必须检查 DBMS 功能，针对不同的 DBMS 以不同的方式执行相同的任务，围绕某些 DBMS 支持的功能（而不是其他 DMS）支持的功能，等等。  
  
 除了开发时间之外，还必须考虑产品生命周期。 如果应用程序设计为一次使用，例如在从一个 DBMS 迁移到另一个 DBMS 时传输数据的应用程序，则使其具有互操作性是没有意义的。 该应用程序将使用一次并丢弃。  
  
 如果应用程序将存在很长时间，则作为可互操作的应用程序进行维护可能更容易。 即使以单个 DBMS 为目标的自定义应用程序也是如此。 原因是可互操作的代码使用有限的数据库功能子集。 即使面对基础 DBMS 的更改，也需要驱动程序来保持这些功能可用。 因此，可互操作的代码可以将应对 DBMS 更改的负担从应用程序开发人员转移到驱动程序开发人员。
