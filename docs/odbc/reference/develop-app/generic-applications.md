---
title: 通用应用程序 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 607676d5370f02ee1d39196bff9261bc897521ee
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305548"
---
# <a name="generic-applications"></a>泛型应用程序
通用应用程序有时执行硬编码任务，例如从数据库检索数据的电子表格。 它们还可能执行各种用户定义的任务，例如允许用户输入和执行 SQL 语句的通用查询应用程序。 通用应用程序的共同点是，它们必须与各种不同的 DBMS 配合使用，并且开发人员事先不知道这些 DBMS 是什么。  
  
 因此，通用应用程序需要高度可互操作。 开发人员必须做出许多选择，权衡功能的互操作性，并且必须编写期望驱动程序支持各种功能的代码。 虽然通用应用程序可能经过调整以使用流行的 DBMS，但它们很少包含特定于驱动程序或特定于 DBMS 的代码。
