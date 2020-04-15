---
title: 测试可互操作的应用程序 |微软文档
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
ms.openlocfilehash: c1d43c7aad2501591c497475f6c250ac33712aa7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307738"
---
# <a name="testing-interoperable-applications"></a>测试交互式应用程序
测试可互操作的应用程序充其量是一项耗时的业务，在最坏的情况下是不可能的，因为新的驱动程序不断出现在市场上。 但是，可以进行合理的测试。 互操作性有限或低的应用程序只需根据保证支持的驱动程序进行测试。 但是，必须针对这些驱动程序进行全面测试。  
  
 高度互操作的应用程序不能对所有驱动程序进行实际测试。 大多数应用程序开发人员能做的最好的事情就是根据少量驱动程序对其进行完全测试，并粗略地针对多个驱动程序。 经过测试的驱动程序应包括应用程序市场中最流行的 DBMS 的驱动程序;如果市场涵盖所有 DBMS，则应测试台式机和服务器 DBMS 的驱动程序。  
  
 测试 ODBC 应用程序时的问题之一是所涉及的组件数量：应用程序本身、驱动程序管理器、驱动程序、DBMS，以及可能的网络软件或网关。 应用程序可以通过**SQLGetDiagField 和 SQLGetDiagRec**发布 ODBC 函数返回的**SQLGetDiagRec**错误消息，从而更轻松地跟踪错误。 这些消息标识发生错误的制造商和组件。 有关详细信息，请参阅[诊断](../../../odbc/reference/develop-app/diagnostics.md)。
