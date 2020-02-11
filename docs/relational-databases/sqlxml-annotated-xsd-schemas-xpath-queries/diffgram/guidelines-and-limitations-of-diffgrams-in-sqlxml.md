---
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
ms.openlocfilehash: eae0b81b3c55a4afe611cd8ed6fdbb495b498c61
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "75246601"
---
# <a name="guidelines-and-limitations-of-diffgrams-in-sqlxml"></a>SQLXML 中 DiffGram 的准则和限制
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  通过 SQLXML 4.0 使用 DiffGram 时请记住以下事项：  
  
-   不应在** \<diffgr**中使用二进制大型对象（BLOB）类型（如**text/ntext**和 images）：在使用 diffgram 的情况下，在中>块之前，因为这将包含它们以用于并发控制。 由于 BLOB 类型的比较限制，这可能导致 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 出现问题。 例如，在 WHERE 子句中使用 LIKE 关键字比较**文本**数据类型的列;但是，对于数据大小大于8K 的 BLOB 类型，比较将失败。  
  
-   由于 BLOB 类型的比较限制， **ntext**数据中的特殊字符可能导致 SQLXML 4.0 问题。 例如，在对**ntext**类型的列进行并发检查时，在** \<diffgr**中使用 "[Serializable]">之前，将失败，并出现以下 SQLOLEDB 错误说明：  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
  
