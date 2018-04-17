---
title: 通用应用程序 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], generic applications
- interoperability [ODBC], levels
- generic applications [ODBC]
ms.assetid: dda2a3c4-76ef-40a6-b3a1-9e95bed61618
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ae9c4bc73af6fdb777abf617cbed8b81eed5c043
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="generic-applications"></a>通用应用程序
通用应用程序有时执行硬编码任务，如电子表格从数据库检索数据。 它们还可能执行的各种用户定义的任务，如一般查询应用程序允许用户输入和执行的 SQL 语句。 通用应用程序具有的共同点是，它们必须处理各种不同 Dbms 和，开发人员不知道事先将哪些这些 Dbms。  
  
 因此，需要高度可互操作的泛型应用程序。 开发人员必须进行多种可供选择，来换取的互操作性功能，并且必须编写代码所需驱动程序以支持各种各样的功能。 虽然通用应用程序可能要优化用于常用 Dbms，它们很少包含特定于驱动程序或特定于 DBMS 的代码。
