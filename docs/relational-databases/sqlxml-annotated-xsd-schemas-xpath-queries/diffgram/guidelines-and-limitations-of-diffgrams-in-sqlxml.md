---
title: SQLXML 中 Diffgram 的准则和限制 |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: cf8689c4-2a63-4d05-b202-21b5ff187d7f
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: d47ff7fb2cfe2cb64a92a17a15b0fff6d4cea1cf
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39542567"
---
# <a name="guidelines-and-limitations-of-diffgrams-in-sqlxml"></a>SQLXML 中 DiffGram 的准则和限制
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  通过 SQLXML 4.0 使用 DiffGram 时请记住以下事项：  
  
-   二进制大型对象 (BLOB) 类型等**text/ntext**和映像不应在 **\<diffgr： 之前 >** 时阻止使用 Diffgram，因为这将使它们在中使用并发控制。 由于 BLOB 类型的比较限制，这可能导致 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 出现问题。 例如，LIKE 关键字用于在 WHERE 子句中的列之间的比较**文本**数据类型; 但是，比较将失败的数据大小大于 8k 的 BLOB 类型。  
  
-   中的特殊字符**ntext**数据可能由于 BLOB 类型的比较限制导致 SQLXML 4.0 出现问题。 例如，使用"[Serializable]"中的 **\<diffgr： 之前 >** DiffGram 时并发检查的列中使用的块**ntext**类型会因以下 SQLOLEDB错误说明：  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
  
