---
title: "数据提供程序 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data providers [ADO]
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 877b9f25-60c4-4ab6-8052-2c28a3849e89
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5a5264398741c58ac6f9aae504237ec1139ecb2c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="data-providers"></a>数据提供程序
数据提供程序表示数据，例如 SQL 数据库、 索引顺序文件、 电子表格、 文档存储和邮件文件的多种不同的源。 提供程序公开使用称为行集的通用抽象统一的数据。  
  
 ADO 是功能强大且灵活，因为它可以连接到任意多个不同的数据提供程序，并且仍然可以公开相同的编程模型，而不考虑任何给定的提供程序的特定功能。 但是，因为每个数据提供程序是唯一的你的应用程序如何与 ADO 交互将因数据提供程序。  
  
 例如，功能和用于访问 Microsoft SQL Server 数据库的 SQL server 的 OLE DB 访问接口的功能有很大差异开来的 Microsoft OLE DB 提供程序用于 Internet 发布，用于访问文件Web 服务器上的存储。

