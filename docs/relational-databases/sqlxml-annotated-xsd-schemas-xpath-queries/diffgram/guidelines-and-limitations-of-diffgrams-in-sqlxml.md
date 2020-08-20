---
description: SQLXML 中 DiffGram 的准则和限制
title: SQLXML 中 DiffGram 的准则和限制
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: cf8689c4-2a63-4d05-b202-21b5ff187d7f
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8a75caa96befa6705d76b5666e3e9a5ef9c131d7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88498503"
---
# <a name="guidelines-and-limitations-of-diffgrams-in-sqlxml"></a>SQLXML 中 DiffGram 的准则和限制
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  通过 SQLXML 4.0 使用 DiffGram 时请记住以下事项：  
  
-   当使用 Diffgram 时，不应在**text/ntext**中的块中使用 (BLOB) 类型的二进制大型对象 **\<diffgr:before>** ，因为这将包含它们以用于并发控制。 由于 BLOB 类型的比较限制，这可能导致 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 出现问题。 例如，在 WHERE 子句中使用 LIKE 关键字比较 **文本** 数据类型的列;但是，对于数据大小大于8K 的 BLOB 类型，比较将失败。  
  
-   由于 BLOB 类型的比较限制， **ntext** 数据中的特殊字符可能导致 SQLXML 4.0 问题。 例如，在对 ntext 类型的列进行并发检查时，在 DiffGram 的块中使用 "[Serializable]" **\<diffgr:before>** 将失败**ntext** ，并出现以下 SQLOLEDB 错误说明：  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
  
