---
description: 目录函数返回的数据
title: 目录函数返回的数据 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], result sets
- functions [ODBC], catalog functions
ms.assetid: 399e1a64-8766-4c44-81ff-445399b7a1de
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4c42319520696060cd52c14c46f968badee27e20
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429359"
---
# <a name="data-returned-by-catalog-functions"></a>目录函数返回的数据
每个目录函数都以结果集的形式返回数据。 此结果集与任何其他结果集没有什么不同。 它通常由预定义的参数化 **SELECT** 语句生成，该语句在驱动程序中进行了硬编码或存储在数据源中的过程中。 有关如何从结果集中检索数据的信息，请参阅 [是否已创建结果集？](../../../odbc/reference/develop-app/was-a-result-set-created.md)。  
  
 每个目录函数的结果集在该函数的参考条目中进行了介绍。 除了列出的列之外，结果集还可以在最后一个预定义列后包含特定于驱动程序的列。 如果驱动程序文档中描述了任何) ，则这些列 (。  
  
 应用程序应将特定于驱动程序的列绑定到结果集的末尾。 也就是说，它们应计算特定于驱动程序的列数，作为最后一列检索到的最后一列的编号（使用 **SQLNumResultCols** ），而不是所需列后出现的列数。 这样就不必在 ODBC 或驱动程序的将来版本中将新列添加到结果集时更改应用程序。 要使此方案生效，驱动程序必须在旧的驱动程序特定列之前添加新的特定于驱动程序的列，以便不会相对于结果集的末尾更改列号。  
  
 在结果集中返回的标识符不带引号，即使它们包含特殊字符。 例如，假设标识符引用字符 (，它是特定于驱动程序的，通过 **SQLGetInfo**) 返回，它是一个双引号 ( ") 并且应付帐款表包含一个名为" 客户名称 "的列。 在 **SQLColumns** 为此列返回的行中，TABLE_NAME 列的值是 "应付帐款"，而不是 "应付帐款"，而 "COLUMN_NAME" 列的值是 "客户名称"，而不是 "customer name"。 若要检索 "应付帐款" 表中客户的名称，应用程序将引用以下名称：  
  
```  
SELECT "Customer Name" FROM "Accounts Payable"  
```  
  
 有关详细信息，请参阅 [带引号的标识符](../../../odbc/reference/develop-app/quoted-identifiers.md)。  
  
 目录函数基于类似 SQL 的授权模型，在该模型中，将根据用户名和密码建立连接，并且仅返回用户具有特权的数据。 不适合此模型的单个文件的密码保护是由驱动程序定义的。  
  
 目录函数返回的结果集几乎无法更新，应用程序不应通过更改这些结果集中的数据来更改数据库的结构。
