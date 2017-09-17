---
title: "答案是 ODBC？ | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], ODBC
ms.assetid: bfa5e6ee-5979-42a9-be6f-a84d1ee7a54c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2ada446a96ecb6fd81d05380c8a29707eb41f8ee
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="is-odbc-the-answer"></a>答案是 ODBC？
在深入了解的互操作性问题之前, 请考虑以下问题： 应用程序应使用 ODBC 根本？ 这看起来有点奇怪问题到 ODBC，指南中提出，但它实际上是，一个合法。 ODBC 未设计为完全替换本机数据库 Api，也不旨在提供在所有情况下的数据库访问。 它旨在提供到数据库的常见界面，用于释放应用程序程序员无需了解和维护多个数据库的链接。  
  
 自定义应用程序是尤其适合本机数据库 Api。 主要原因是，自定义应用程序通常使用单个 DBMS，无需进行互操作。 本机数据库 Api 可能会执行更好地于 ODBC 的公开特定 DBMS 的功能，并可能会公开不由 ODBC 公开的功能。 此外，因为自定义应用程序的开发人员熟悉通常其 DBMS 的本机数据库 API，存在很少需要了解 ODBC。 但是，值得注意的是，对于某些 Dbms ODBC 是本机数据库 API。  
  
 因此，哪些应用程序是否适用于 ODBC 的候选项？ 最佳候选项为使用多个 DBMS 应用程序。 这包括泛型和垂直的几乎所有应用程序。 它还包括大量的自定义应用程序。 使用多个不同 Dbms 的自定义应用程序是更轻松、 清理程序使用 ODBC 比使用多个本机 Api 编写的示例。 并且使用 ODBC 编写的自定义应用程序可以更轻松地迁移公司将其从一个 DBMS 移动到另一个，或部署针对不同 Dbms 对同一个应用程序。
