---
title: ADO 基础 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: d6a66928-e68f-4c38-b87a-838c5de50a28
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 75f5030f8faa5aa5d8e8a0f6bcb6d72b186c8448
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67926061"
---
# <a name="ado-fundamentals"></a>ADO 基础知识
ADO 为开发人员提供了一个功能强大的逻辑对象模型，可通过 OLE DB 系统接口以编程方式访问、编辑和更新各种数据源中的数据。 ADO 最常见的用法是查询关系数据库中的一个或多个表，检索并显示应用程序中的结果，并可能让用户进行更改并保存对数据所做的更改。 其他任务包括：  
  
-   使用 SQL 查询数据库并显示结果。  
  
-   通过 Internet 访问文件存储中的信息。  
  
-   操作电子邮件系统中的邮件和文件夹。  
  
-   将数据库中的数据保存到 XML 文件中。  
  
-   执行 XML 所述的命令和检索 XML 流。  
  
-   将数据保存到二进制或 XML 流中。  
  
-   允许用户查看和更改数据库表中的数据。  
  
-   创建和重用参数化的数据库命令。  
  
-   执行存储过程。  
  
-   动态创建一个名为**记录集**的灵活结构，用于保存、导航和处理数据。  
  
-   执行事务性数据库操作。  
  
-   基于运行时条件筛选和排序数据库信息的本地副本。  
  
-   创建和操作数据库中的分层结果。  
  
-   将数据库字段绑定到识别数据的组件。  
  
-   创建远程、断开连接的**记录集**。  
  
 ADO 公开多种选项和设置，以提供这种灵活性。 因此，务必要采取一种方法来了解如何在应用程序中使用 ADO，将每个目标分解为可管理的部分。  
  
 大多数使用 ADO 的应用程序都涉及四个主要操作：获取数据、检查数据、编辑数据和更新数据。 本部分稍后将详细介绍这些操作。  
  
 但是，在讨论这些详细信息之前，我们将概述 ADO 对象模型和一个简单的 ADO 应用程序，该应用程序是使用 Microsoft® Visual Basic®编写的，并执行四个主要 ADO 操作：  
  
-   [ADO 对象和集合](../../../ado/guide/data/ado-objects-and-collections.md)  
  
-   [HelloData：简单的 ADO 应用程序](../../../ado/guide/data/hellodata-a-simple-ado-application.md)  
  
-   [OLE DB 提供程序](../../../ado/guide/data/ole-db-providers-ado.md)  
  
-   [错误](../../../ado/guide/data/errors-ado.md)
