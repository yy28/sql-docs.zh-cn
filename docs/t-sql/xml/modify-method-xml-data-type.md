---
title: modify() 方法（xml 数据类型）| Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- modify() method
- modify method
ms.assetid: 52430735-51f4-46d1-a308-9aecf8648fda
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7182961996510fcded86a3e1d218d482eb834e63
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85731065"
---
# <a name="modify-method-xml-data-type"></a>modify() 方法（xml 数据类型）
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  修改 XML 文档的内容。 使用此方法修改 xml 类型变量或列的内容  。 此方法使用 XML DML 语句在 XML 数据中插入、更新或删除节点。 xml 数据类型的 modify() 方法只能在 UPDATE 语句的 SET 子句中使用   。  
  
## <a name="syntax"></a>语法  
  
```  
  
modify (XML_DML)  
```  
  
## <a name="arguments"></a>参数  
 XML_DML  
 是 XML 数据操作语言 (DML) 中的字符串。 将根据此表达式来更新 XML 文档。  
  
> [!NOTE]  
>  如果针对 null 值或以 null 值表示的结果调用 modify() 方法，则会返回错误  。  
  
## <a name="examples"></a>示例  
 modify() 方法需要使用 XML 数据操作语言 (DML) 中的字符串，因此有关 modify() 的示例包含在说明 XML DML 语句的主题中   。 有关这些示例，请参阅[插入 (XML DML)](../../t-sql/xml/insert-xml-dml.md)、[删除 (XML DML)](../../t-sql/xml/delete-xml-dml.md) 和[替换 (XML DML) 的值](../../t-sql/xml/replace-value-of-xml-dml.md)。  
  
## <a name="see-also"></a>另请参阅  
 [创建 XML 数据的实例](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 数据类型方法](../../t-sql/xml/xml-data-type-methods.md)   
 [XML 数据修改语言 (XML DML)](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
