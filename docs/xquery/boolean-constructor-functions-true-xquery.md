---
title: "true 函数 (XQuery) |Microsoft 文档"
ms.custom: 
ms.date: 08/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- fn:true function
- true function
ms.assetid: 318e370d-0444-4812-afe4-307df7ef9f3b
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 56a05212956cc9e749fe7c1ccf090daec30f0dfc
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="boolean-constructor-functions---true-xquery"></a>布尔构造函数-true (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回 xs:boolean 值 True。 这等效于 `xs:boolean("1")`。  
  
## <a name="syntax"></a>语法  
  
```  
fn:true() as xs:boolean  
```  
  
## <a name="examples"></a>示例  
 本主题提供对存储在各种的 XML 实例的 XQuery 示例**xml** AdventureWorks 数据库中的类型列。  
  
### <a name="a-using-the-true-xquery-boolean-function"></a>A. 使用 XQuery 布尔函数 true()  
 下面的示例查询一个非类型化**xml**变量。 中的表达式**value （)**方法返回布尔值**true()**如果"aaa"的属性值。 **Value （)**方法**xml**数据类型将的布尔值转换为位，并将其返回。  
  
```  
DECLARE @x XML  
SET @x= '<ROOT><elem attr="aaa">bbb</elem></ROOT>'  
select @x.value(' if ( (/ROOT/elem/@attr)[1] eq "aaa" ) then fn:true() else fn:false() ', 'bit')  
go  
-- result = 1  
```  
  
 在下面的示例中，指定的查询针对类型化**xml**列。 `if` 表达式将检查 <`ROOT`> 元素的类型化布尔值，并相应地返回结构化 XML。 该示例执行以下操作：  
  
-   创建一个定义 xs:boolean 类型的 <`ROOT`> 元素的 XML 架构集合。  
  
-   创建一个具有类型化表**xml**通过使用 XML 架构集合的列。  
  
-   将 XML 实例保存在列中并查询它。  
  
```  
-- Drop table if exist  
--DROP TABLE T  
--go  
DROP XML SCHEMA COLLECTION SC  
go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
targetNamespace="QNameXSD" >  
      <element name="ROOT" type="boolean" nillable="true"/>  
</schema>'  
go  
CREATE TABLE T (xmlCol XML(SC))  
go  
-- following OK  
insert into T values ('<ROOT xmlns="QNameXSD">true</ROOT>')  
 go  
-- Retrieve the local name.   
SELECT xmlCol.query('declare namespace a="QNameXSD";   
   if (/a:ROOT[1] eq true()) then  
       <result>Found boolean true</result>  
   else  
       <result>Found boolean false</result>')  
  
FROM T  
-- result = <result>Found boolean true</result>  
-- Clean up  
DROP TABLE T  
go  
DROP XML SCHEMA COLLECTION SC  
go  
```  
  
## <a name="see-also"></a>另请参阅  
 [布尔构造函数 &#40;XQuery &#41;](http://msdn.microsoft.com/library/fa907f39-d4b7-4495-b829-c788928e0f64)  
  
  
