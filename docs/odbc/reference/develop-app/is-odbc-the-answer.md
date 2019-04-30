---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f90f2395eac5dce76848d7bc309f1a3d5ce289f9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63179892"
---
# <a name="is-odbc-the-answer"></a>需要 ODBC？
在深入探讨的互操作性问题之前, 请考虑以下问题：应用程序应在所有使用 ODBC？ 这看起来有点奇怪问题到 ODBC，指南中提出，但它实际上是，合法。 ODBC 不用于完全取代本机数据库 Api，也不旨在提供在所有情况下的数据库访问权限。 它旨在提供一个公共接口对数据库和要用于免费应用程序程序员无需了解和维护多个数据库的链接。  
  
 自定义应用程序是本机数据库 Api 的首要候选对象。 主要原因是自定义应用程序通常使用单个 DBMS 工作，并具有无需进行互操作。 本机数据库 Api 可能会更好地晚于 ODBC 的公开特定 DBMS 的功能和可能会公开不通过 ODBC 公开的功能。 此外，由于自定义应用程序的开发人员通常熟悉其 DBMS 本机数据库 API，是几乎不需要了解 ODBC。 但是，有趣的是要注意，对于某些 Dbms，ODBC 是本机数据库 API。  
  
 那么哪些应用程序是用于 ODBC 的候选项呢？ 最佳候选项是使用多个 DBMS 的应用程序。 这包括泛型和垂直的几乎所有应用程序。 它还包括大量的自定义应用程序。 例如，使用多个不同的 Dbms 的自定义应用程序是更轻松、 更简洁、 更易使用 ODBC 比使用多个本机 Api 编写。 和通过 ODBC 编写的自定义应用程序变得更容易迁移一家公司将其从一个 DBMS 移到另一个，或将针对不同 Dbms 相同的应用程序部署。
