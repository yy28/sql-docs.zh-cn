---
title: 数据访问接口 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925658"
---
# <a name="data-providers"></a>数据提供程序
数据访问接口表示不同的数据源，例如 SQL 数据库、索引顺序文件、电子表格、文档存储和邮件文件。 提供程序使用称为行集的通用抽象来统一公开数据。  
  
 ADO 的功能强大且灵活，因为它可以连接到多个不同的数据访问接口中的任何一种，并且仍公开相同的编程模型，而与任何给定提供程序的特定功能无关。 但是，由于每个数据提供程序都是唯一的，因此，应用程序与 ADO 交互的方式将因数据访问接口而异。  
  
 例如，用于访问 Microsoft SQL Server 数据库的 SQL Server 的 OLE DB 提供程序的功能和功能与用于访问 Web 服务器上的文件存储的 Microsoft OLE DB 提供程序的功能和用于 Internet 发布的提供程序的功能大不相同。
