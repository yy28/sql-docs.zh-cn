---
title: 在产品周期长度 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], product cycle
- length of the product cycle [ODBC]
ms.assetid: 4d08d886-6d8b-40fd-8544-13032f4bf6c7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7865238b62dd8228f2902d86d8f6fbaf9efc0b7f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="length-of-the-product-cycle"></a>在产品周期的长度
关于互操作性最后一个问题是时间。 通常在开发可互操作应用程序时，所用时间长于开发一个 noninteroperable。 原因是应用程序必须检查 DBMS 功能、 为不同 Dbms 以不同的方式执行相同的任务、 解决某些 Dbms 而非任何其他支持的功能和等。  
  
 除了开发时间外，还必须考虑产品生存期。 如果应用程序设计为使用一次，例如当从一个 DBMS 迁移到另一个字符串，在将数据传输的应用程序则没有必要再使其可互操作。 应用程序将使用一次，并且可以被丢弃。  
  
 如果应用程序将存在很长时间，则可能是更易维护为一个可互操作的应用程序。 这是 true，即使对于具有单一 DBMS 作为目标的自定义应用程序。 原因是可互操作的代码使用数据库功能的有限的子集。 该驱动程序需要保留这些功能可用，即使在遇到时对基础 DBMS 的更改。 因此，可互操作的代码可以解决的更改的负担 DBMS 将从切换到应用程序开发人员向驱动程序开发人员。
