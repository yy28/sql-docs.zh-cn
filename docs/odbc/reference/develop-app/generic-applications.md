---
title: 通用应用程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], generic applications
- interoperability [ODBC], levels
- generic applications [ODBC]
ms.assetid: dda2a3c4-76ef-40a6-b3a1-9e95bed61618
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 59110f66c512845ff5ce1f2f246c05c63fa755b9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63061495"
---
# <a name="generic-applications"></a>泛型应用程序
通用应用程序有时会执行硬编码任务，如从数据库检索数据电子表格。 它们还可能执行的各种用户定义的任务，例如允许用户输入和执行 SQL 语句的一般查询应用程序。 通用应用程序具有的共同点是它们必须适用于各种不同的 Dbms 和，开发人员不会预先不知道这些 Dbms 是怎样的。  
  
 因此，需要高度可互操作泛型应用程序。 开发人员必须做出很多选择，来换取的互操作性功能，并且必须编写代码所需驱动程序以支持范围广泛的功能。 尽管通用应用程序可能会经过调整，以使用受欢迎的 Dbms，但很少包含特定于驱动程序或特定于 DBMS 的代码。
