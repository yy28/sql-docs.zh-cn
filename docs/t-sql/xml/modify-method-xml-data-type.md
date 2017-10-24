---
title: "modify （) 方法 (xml 数据类型) |Microsoft 文档"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- modify() method
- modify method
ms.assetid: 52430735-51f4-46d1-a308-9aecf8648fda
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 81838bf62f9b2c92dce4df8a167785fdfbf7abb2
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="modify-method-xml-data-type"></a>modify() 方法（xml 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  修改 XML 文档的内容。 使用此方法可修改的内容**xml**类型变量或列。 此方法使用 XML DML 语句在 XML 数据中插入、更新或删除节点。 **Modify （)**方法**xml**数据类型仅可在 UPDATE 语句的 SET 子句。  
  
## <a name="syntax"></a>语法  
  
```  
  
modify (XML_DML)  
```  
  
## <a name="arguments"></a>参数  
 XML_DML  
 是 XML 数据操作语言 (DML) 中的字符串。 将根据此表达式来更新 XML 文档。  
  
> [!NOTE]  
>  如果返回错误**modify （)**方法调用对 null 值，或导致 null 值。  
  
## <a name="examples"></a>示例  
 因为**modify （)**方法需要字符串中 XML 数据操作语言 (DML) 中的示例**modify （)**包含在描述 XML DML 语句的主题。 这些示例中，请参阅[insert &#40;XML DML &#41;](../../t-sql/xml/insert-xml-dml.md)，[删除 &#40;XML DML &#41;](../../t-sql/xml/delete-xml-dml.md)和[替换值的 &#40;XML DML &#41;](../../t-sql/xml/replace-value-of-xml-dml.md).  
  
## <a name="see-also"></a>另请参阅  
 [创建 XML 数据的实例](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 数据类型方法](../../t-sql/xml/xml-data-type-methods.md)   
 [XML 数据修改语言 &#40;XML DML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  

