---
title: 自定义应用程序 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], custom applications
- custom applications [ODBC]
- interoperability [ODBC], levels
ms.assetid: f28178d9-ecd6-4e8c-9644-9bb624999dcb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: df00a748ee4d5e3a63b32c95449417a1057b58e1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305278"
---
# <a name="custom-applications"></a>自定义应用程序
自定义应用程序通常为几个 DBMS 执行特定任务。 例如，应用程序可能从单个 DBMS 检索数据并生成报告，或者它可能在多个 DBMS 之间传输数据。 这些应用程序的共同点是，这些 DBMS 在编写应用程序之前是已知的，并且不太可能在应用程序的生命周期内更改。  
  
 因此，自定义应用程序只需要很少或根本没有互操作性。 应用程序开发人员可以为每个 DBMS 选择一个驱动程序，并直接向这些驱动程序编写代码。 应用程序可以安全地包含特定于驱动程序的代码，以利用这些驱动程序的功能，甚至可能调用本机数据库 API 以使用 ODBC 不支持的功能。  
  
 大多数自定义应用程序的主要互操作性问题是目标 DBMS 将来是否会发生变化。 如果是这样，可以通过编写更多的可互操作代码来简化此过程。 然而，这种DBMS的这种变化是罕见的，通常需要大量的工作。 因此，自定义应用程序的开发人员很少选择以牺牲功能为代价来增加互操作性;他们通常选择在更改 DBMS 时重新编码该功能。
