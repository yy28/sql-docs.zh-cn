---
title: 自定义应用程序 |Microsoft 文档
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
- interoperability [ODBC], custom applications
- custom applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: f28178d9-ecd6-4e8c-9644-9bb624999dcb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8f2a4eab813bc691fd435dc00778cbfe41c8bdcc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="custom-applications"></a>自定义应用程序
自定义应用程序通常为几个 Dbms 执行特定任务。 例如，应用程序可能会从单个 DBMS 中检索数据并生成报告，或它可能在几个 Dbms 之间的数据传输。 这些应用程序具有共同点是这些 Dbms 写入应用程序之前已知的而是可能会更改应用程序的生命周期。  
  
 因此，自定义应用程序需要很少或没有互操作性。 应用程序开发人员可以为每个 DBMS 和直接向这些驱动程序的代码选择单独的驱动程序。 应用程序可以安全地包含特定于驱动程序的代码，来利用这些驱动程序的功能，并甚至可能会使对本机数据库 API 调用，以使用不支持 ODBC 的功能。  
  
 大多数自定义应用程序的主要互操作性问题是目标 Dbms 将在将来更改。 如果是这样，可以通过开始编写互操作性更代码简化此过程。 但是，此类更改的 Dbms 很少见，通常需要大量的工作。 因此，开发人员自定义应用程序的极少数情况下选择以提高互操作性，代价是牺牲这样的功能。它们通常选择在更改 Dbms 时重新编码该功能。
