---
title: 自定义应用程序 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6ab470951162b5e4035c1253ed4ce425356ad8ec
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63042523"
---
# <a name="custom-applications"></a>自定义应用程序
自定义应用程序通常执行特定任务的几个 Dbms。 例如，应用程序可能检索单个 DBMS 中的数据并生成报告，或者它可能在多个 Dbms 之间的数据传输。 这些应用程序具有的共同点是这些 Dbms 之前编写的应用程序已知的且不太可能更改应用程序的生命周期。  
  
 因此，自定义应用程序需要很少或没有互操作性。 应用程序开发人员可以选择单个驱动程序为每个 DBMS 和直接向这些驱动程序的代码。 应用程序可以安全地包含特定于驱动程序的代码能够利用这些驱动程序的功能，并甚至可能会使对本机数据库 API 调用，以使用不支持 ODBC 的功能。  
  
 大多数自定义应用程序的主互操作性问题是目标 Dbms 将在以后更改。 如果是这样，可以通过开始编写更可互操作代码来简化此过程。 但是，此类更改的 Dbms 情况很少见，通常需要大量的工作。 因此，自定义应用程序的开发人员很少选择增加牺牲功能; 互操作性他们通常选择在更改 Dbms 时对该功能重新编码。
