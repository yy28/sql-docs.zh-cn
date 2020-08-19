---
description: 自定义应用程序
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 56829c72264ba128554af0534e8a6bfa16254142
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429389"
---
# <a name="custom-applications"></a>自定义应用程序
自定义应用程序通常会对几个 Dbms 执行特定任务。 例如，应用程序可能检索单个 DBMS 中的数据并生成报告，或者可以在多个 Dbms 之间传输数据。 这些应用程序的常见之处在于，这些 Dbms 是在编写应用程序之前已知的，在应用程序的整个生命周期内不太可能更改。  
  
 因此，自定义应用程序需要很少或无互操作性。 应用程序开发人员可以为每个 DBMS 和代码直接选择单一的驱动程序和代码。 应用程序可以安全地包含特定于驱动程序的代码，以利用这些驱动程序的功能，甚至还可以调用本机数据库 API 来使用 ODBC 不支持的功能。  
  
 大多数自定义应用程序的主要互操作性问题是目标 Dbms 将来是否会更改。 如果是这样，可以通过编写更具互操作性的代码来简化此过程。 但是，这种更改 Dbms 非常罕见，通常需要大量工作。 因此，自定义应用程序的开发人员很少选择提高互操作性，代价是功能，它们通常会在更改 Dbms 时选择重编码该功能。
