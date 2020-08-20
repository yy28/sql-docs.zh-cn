---
description: 需要 ODBC？
title: 需要 ODBC？ | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], ODBC
ms.assetid: bfa5e6ee-5979-42a9-be6f-a84d1ee7a54c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7a51c4248a041d65f00ec1846f60788cded68f7b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476599"
---
# <a name="is-odbc-the-answer"></a>需要 ODBC？
在深入了解互操作性问题之前，请考虑以下问题：应用程序是否应同时使用 ODBC？ 这似乎是一个对 ODBC 的指导，但实际上是合法的问题。 ODBC 并非专门用于完全取代本机数据库 Api，也不是为了在所有情况下提供数据库访问。 它旨在提供数据库的通用接口，旨在使应用程序程序员无需了解并维护指向多个数据库的链接。  
  
 自定义应用程序是本机数据库 Api 的最佳候选项。 主要原因是自定义应用程序通常使用单个 DBMS，无需进行互操作。 本机数据库 Api 的工作方式可能比 ODBC 公开特定 DBMS 的功能更好，可能会公开 ODBC 未公开的功能。 此外，由于自定义应用程序的开发人员通常熟悉其 DBMS 的本机数据库 API，因此很少有了解 ODBC。 不过，请注意，对于某些 Dbms，ODBC 是本机数据库 API。  
  
 那么，哪些应用程序是 ODBC 的候选项？ 最佳候选项是可与多个 DBMS 一起使用的应用程序。 这包括几乎所有的泛型和垂直应用程序。 它还包括许多自定义应用程序。 例如，使用多个不同 Dbms 的自定义应用程序与使用多个本机 Api 编写的 ODBC 更简单、更简洁。 随着公司从一个 DBMS 移到另一个 DBMS 或针对不同 Dbms 部署相同的应用程序，使用 ODBC 编写的自定义应用程序更容易迁移。
