---
title: 数据提供程序 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data providers [ADO]
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 877b9f25-60c4-4ab6-8052-2c28a3849e89
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 40506ec971782c5e9108a34fd240faabcc2756b2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925658"
---
# <a name="data-providers"></a>数据提供程序
数据提供程序表示不同源的数据，例如 SQL 数据库、 编制索引顺序文件、 电子表格、 文档存储和邮件文件。 提供程序公开使用称为行集的常见抽象来统一的数据。  
  
 ADO 是功能强大且灵活，因为它可以连接到任意多个不同的数据提供程序，并仍公开了相同的编程模型，而不考虑任何给定的提供程序的特定功能。 但是，每个数据提供程序是唯一的因为应用程序与 ADO 的交互会因数据提供程序。  
  
 例如，对于 SQL Server，用于访问 Microsoft SQL Server 数据库的 OLE DB 访问接口的功能有很大差异的 Microsoft OLE DB 访问接口用于 Internet 发布，用于访问文件Web 服务器上的存储。
