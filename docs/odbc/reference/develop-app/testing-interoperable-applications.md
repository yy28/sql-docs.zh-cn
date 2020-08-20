---
description: 测试交互式应用程序
title: 测试互操作应用程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], testing interoperable applications
- testing interoperable applications [ODBC]
ms.assetid: 489083cb-8430-40be-9ef2-d75b9a2eea88
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: feebbe5914e9da1e414f5c77a1a69bc0a6e0e7b1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487520"
---
# <a name="testing-interoperable-applications"></a>测试交互式应用程序
测试互操作性应用程序是一种非常耗时的业务，而且可能会因为新的驱动程序不断出现在市场上而无法实现。 但是，可以合理地测试。 具有有限或低互操作性要求的应用程序仅需根据它们可支持的驱动程序进行测试。 但是，必须针对这些驱动程序对它们进行全面测试。  
  
 高度可互操作的应用程序不能完全针对所有驱动程序进行测试。 大多数应用程序开发人员的最佳做法是，对少量的驱动程序和 cursorily 进行更多的测试。 经过测试的驱动程序应包含应用程序市场中最流行的 Dbms 最流行的驱动程序;如果市场覆盖了所有 Dbms，则应该测试桌面和服务器 Dbms 的驱动程序。  
  
 测试 ODBC 应用程序中的问题之一是所涉及的组件数：应用程序本身、驱动程序管理器、驱动程序、DBMS，以及可能的网络软件或网关。 通过使用 **SQLGetDiagField** 和 **SQLGetDiagRec**发布 ODBC 函数返回的错误消息，应用程序可以更轻松地跟踪错误。 这些消息标识发生错误的制造商和组件。 有关详细信息，请参阅 [诊断](../../../odbc/reference/develop-app/diagnostics.md)。
