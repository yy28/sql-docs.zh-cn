---
title: "指导原则和限制在 SQLXML Diffgram |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: cf8689c4-2a63-4d05-b202-21b5ff187d7f
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2af871b240d318aaa027402a52a9c31498521b99
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2018
---
# <a name="guidelines-and-limitations-of-diffgrams-in-sqlxml"></a>SQLXML 中 DiffGram 的准则和限制
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
通过 SQLXML 4.0 使用 DiffGram 时请记住以下事项：  
  
-   二进制大型对象 (BLOB) 类型类似**文本/ntext**和映像不应在 **\<diffgr： 之前 >**时阻止使用 Diffgram，因为这会将其包含在中使用并发控制。 由于 BLOB 类型的比较限制，这可能导致 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 出现问题。 例如，一 LIKE 关键字的 WHERE 子句中使用，用于比较的各个栏之间时**文本**数据类型; 但是，比较将失败，对于数据的大小大于 8 K 的 BLOB 类型。  
  
-   中的特殊字符**ntext**数据会导致问题，SQLXML 4.0 由于上用于 BLOB 类型的比较的限制。 例如，使用"[Serializable]"中的 **\<diffgr： 之前 >** DiffGram 时使用并发检查的列中的块**ntext**类型会因以下 SQLOLEDB错误说明：  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
  
