---
title: modify() 方法（xml 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|xml
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
manager: craigg
ms.openlocfilehash: 01ad2afc24c09cdd6a05189335f1e0d6827d24c4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="modify-method-xml-data-type"></a>modify() 方法（xml 数据类型）
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  修改 XML 文档的内容。 使用此方法修改 xml 类型变量或列的内容。 此方法使用 XML DML 语句在 XML 数据中插入、更新或删除节点。 xml 数据类型的 modify() 方法只能在 UPDATE 语句的 SET 子句中使用。  
  
## <a name="syntax"></a>语法  
  
```  
  
modify (XML_DML)  
```  
  
## <a name="arguments"></a>参数  
 XML_DML  
 是 XML 数据操作语言 (DML) 中的字符串。 将根据此表达式来更新 XML 文档。  
  
> [!NOTE]  
>  如果针对 null 值或以 null 值表示的结果调用 modify() 方法，则会返回错误。  
  
## <a name="examples"></a>示例  
 modify() 方法需要使用 XML 数据操作语言 (DML) 中的字符串，因此有关 modify() 的示例包含在说明 XML DML 语句的主题中。 有关这些示例，请参阅[插入 (XML DML)](../../t-sql/xml/insert-xml-dml.md)、[删除 (XML DML)](../../t-sql/xml/delete-xml-dml.md) 和[替换 (XML DML) 的值](../../t-sql/xml/replace-value-of-xml-dml.md)。  
  
## <a name="see-also"></a>另请参阅  
 [创建 XML 数据的实例](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 数据类型方法](../../t-sql/xml/xml-data-type-methods.md)   
 [XML 数据修改语言 (XML DML)](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
