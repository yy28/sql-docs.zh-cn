---
title: 测试交互式应用程序 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 509dd17efeeb982c51938d7a18fad99a2e84ba5b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63148932"
---
# <a name="testing-interoperable-applications"></a>测试交互式应用程序
测试交互式应用程序是最耗时的业务和最坏的情形是不可能因为在市场上不断出现新的驱动程序。 但是，可能会合理程度的测试。 具有有限的或较低的互操作性的应用程序只需要针对可确保支持这些驱动程序测试。 但是，它们必须进行完全测试针对这些驱动程序。  
  
 高度可互操作应用程序针对的所有驱动程序不能实际进行测试。 大多数应用程序开发人员可以执行操作的最佳是其完全针对少量的驱动程序和几个 cursorily 进行测试。 经过测试的驱动程序应包括最常用的驱动程序的应用程序的市场; 中最受欢迎的 Dbms如果市场涵盖所有 Dbms，台式机和服务器 Dbms 的驱动程序应进行测试。  
  
 测试 ODBC 应用程序中的问题之一是涉及的组件数： 应用程序本身、 驱动程序管理器、 驱动程序、 DBMS 和可能是网络软件或网关。 应用程序可以轻松地通过发布通过 ODBC 函数返回的错误消息来跟踪错误**SQLGetDiagField**并**SQLGetDiagRec**。 这些消息确定的制造商和组件发生错误。 有关详细信息，请参阅[诊断](../../../odbc/reference/develop-app/diagnostics.md)。
