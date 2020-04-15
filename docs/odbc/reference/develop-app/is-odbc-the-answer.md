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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f3716acbcc1b8ea648b5edc03e277983936da557
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288088"
---
# <a name="is-odbc-the-answer"></a>需要 ODBC？
在深入探讨互操作性问题之前，请考虑以下问题：应用程序是否应使用 ODBC？ 在 ODBC 指南中，这似乎是一个奇怪的问题，但事实上，这是一个合理的问题。 ODBC 并非旨在完全替换本机数据库 API，也不是旨在在所有情况下提供数据库访问。 它旨在为数据库提供一个通用接口，旨在使应用程序程序员不必了解和维护到多个数据库的链接。  
  
 自定义应用程序是本机数据库 API 的主要候选项。 主要原因是自定义应用程序通常使用单个 DBMS，并且不需要互操作。 本机数据库 API 在公开特定 DBMS 的功能方面可能比 ODBC 做得更好，并且可能会公开 ODBC 未公开的功能。 此外，由于自定义应用程序的开发人员通常熟悉其 DBMS 的本机数据库 API，因此几乎没有理由学习 ODBC。 但是，值得注意的是，对于某些 DBMS，ODBC 是本机数据库 API。  
  
 那么，哪些应用程序是 ODBC 的候选应用程序？ 最佳候选是使用多个 DBMS 的应用程序。 这包括几乎所有通用和垂直应用程序。 它还包括许多自定义应用程序。 例如，使用多个不同 DBMS 的自定义应用程序与多个本机 API 相比，使用 ODBC 编写起来要容易得多、更简洁。 当公司从一个 DBMS 移动到另一个 DBMS 或针对不同的 DBMS 部署同一应用程序时，使用 ODBC 编写的自定义应用程序更易于迁移。
