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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 607676d5370f02ee1d39196bff9261bc897521ee
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305548"
---
# <a name="generic-applications"></a>泛型应用程序
一般的应用程序有时会执行硬编码任务，如电子表格从数据库检索数据。 它们还可能执行各种用户定义的任务，例如一般查询应用程序，允许用户输入和执行 SQL 语句。 常见的一般应用程序是，它们必须使用各种不同的 Dbms，开发人员不知道这些 Dbms 将是什么。  
  
 因此，一般的应用程序需要高度可互操作。 开发人员必须做出很多选择，权衡功能的互操作性，并且必须编写需要驱动程序支持各种功能的代码。 尽管一般的应用程序可能会进行优化，以便与流行的 Dbms 一起使用，但它们极少包含驱动程序特定或 DBMS 特定的代码。
