---
title: SQLXML 中 Diffgram 的准则和限制 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: cf8689c4-2a63-4d05-b202-21b5ff187d7f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4ca731cab8a88364b3b87dfc282c10fa14ebf283
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52804339"
---
# <a name="guidelines-and-limitations-of-diffgrams-in-sqlxml"></a>SQLXML 中 DiffGram 的准则和限制
  通过 SQLXML 4.0 使用 DiffGram 时请记住以下事项：  
  
-   在使用 DiffGram 时，不应在 `text/ntext` 块中使用诸如 `<diffgr:before>` 和 image 的二进制大型对象 (BLOB) 类型，因为这将使它们用在并发控制中。 由于 BLOB 类型的比较限制，这可能导致 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 出现问题。 例如，在 WHERE 子句中使用 LIKE 关键字比较 `text` 数据类型的列；不过，对于数据大小大于 8K 的 BLOB 类型，比较将失败。  
  
-   由于 BLOB 类型的比较限制，`ntext` 数据中的特殊字符可能导致 SQLXML 4.0 出现问题。 例如，在对 `<diffgr:before>` 类型的列进行并发检查时，如果在 DiffGram 的 `ntext` 块中使用“[Serializable]”，检查将失败，并显示以下 SQLOLEDB 错误说明：  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
  
