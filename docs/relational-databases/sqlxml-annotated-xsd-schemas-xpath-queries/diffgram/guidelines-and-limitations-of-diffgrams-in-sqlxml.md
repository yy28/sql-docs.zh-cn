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
ms.openlocfilehash: 113090c317e88d3e9a7e7db2bfcb7d4d14b4ea1f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85650063"
---
# <a name="guidelines-and-limitations-of-diffgrams-in-sqlxml"></a>SQLXML 中 DiffGram 的准则和限制
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  通过 SQLXML 4.0 使用 DiffGram 时请记住以下事项：  
  
-   当使用 Diffgram 时，不应在中的块中使用二进制大型对象（BLOB）类型（如**text/ntext**和 images） **\<diffgr:before>** ，因为这将包含它们以用于并发控制。 由于 BLOB 类型的比较限制，这可能导致 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 出现问题。 例如，在 WHERE 子句中使用 LIKE 关键字比较**文本**数据类型的列;但是，对于数据大小大于8K 的 BLOB 类型，比较将失败。  
  
-   由于 BLOB 类型的比较限制， **ntext**数据中的特殊字符可能导致 SQLXML 4.0 问题。 例如，在对 ntext 类型的列进行并发检查时，在 DiffGram 的块中使用 "[Serializable]" **\<diffgr:before>** 将失败**ntext** ，并出现以下 SQLOLEDB 错误说明：  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
  
