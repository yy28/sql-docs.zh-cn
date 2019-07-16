---
title: 展开的 QName (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- expanded-QName function
- fn:expanded-QName function
ms.assetid: b8377042-95cc-467b-9ada-fe43cebf4bc3
author: rothja
ms.author: jroth
ms.openlocfilehash: 7c50409ea35809c52de718a8281bf76f75a5a0e0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004582"
---
# <a name="functions-related-to-qnames---expanded-qname"></a>与 QName 相关的函数 - expanded-QName
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回与命名空间中指定 URI 的 xs: qname 类型值 *$paramURI*中指定的本地名称和 *$paramLocal*。 如果 *$paramURI*是空字符串或空序列，它表示无命名空间。  
  
## <a name="syntax"></a>语法  
  
```  
fn:expanded-QName($paramURI as xs:string?, $paramLocal as xs:string?) as xs:QName?  
```  
  
## <a name="arguments"></a>参数  
 *$paramURI*  
 QName 的命名空间 URI。  
  
 *$paramLocal*  
 QName 的本地名称部分。  
  
## <a name="remarks"></a>备注  
 以下规则适用于**expanded-qname （)** 函数：  
  
-   如果 *$paramLocal*指定值不是 xs: ncname 类型的正确词汇格式中，会返回空序列，并表示动态错误。  
  
-   在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中不支持从 xs:QName 类型转换为任何其他类型。 因此， **expanded-qname （)** 函数不能用于 XML 构造。 例如，当构造节点（如 `<e> expanded-QName(...) </e>`）时，其值就必须是非类型化的。 这就要求您将 `expanded-QName()` 返回的 xs:QName 类型值转换为 xdt:untypedAtomic。 但是，不支持此操作。 在本主题的后面的示例中给出了一种解决方案。  
  
-   您可以修改或比较现有的 QName 类型值。 例如，`/root[1]/e[1] eq expanded-QName("http://nsURI" "myNS")`元素的值进行比较 <`e`>，返回的 qname **expanded-qname （)** 函数。  
  
## <a name="examples"></a>示例  
 本主题提供了一些针对 XML 实例存储在各种中的 XQuery 示例**xml**类型列中的[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]数据库。  
  
### <a name="a-replacing-a-qname-type-node-value"></a>A. 替换 QName 类型节点值  
 此示例说明了如何修改 QName 类型的元素节点的值。 该示例执行以下操作：  
  
-   创建定义 QName 类型的元素的 XML 架构集合。  
  
-   创建一个包含**xml**使用 XML 架构集合的类型列。  
  
-   将 XML 实例保存在表中。  
  
-   使用**modify （)** 要修改的实例中的 QName 类型元素的值的 xml 数据类型的方法。 **Expanded-qname （)** 函数用于生成新的 QName 类型值。  
  
```  
-- If XML schema collection (if exists)  
-- drop xml schema collection SC  
-- go  
-- Create XML schema collection  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
    xmlns:xs="http://www.w3.org/2001/XMLSchema"   
    targetNamespace="QNameXSD"   
      xmlns:xqo="QNameXSD" elementFormDefault="qualified">  
      <element name="Root" type="xqo:rootType" />  
      <complexType name="rootType">  
            <sequence minOccurs="1" maxOccurs="1">  
                        <element name="ElemQN" type="xs:QName" />  
            </sequence>  
      </complexType>  
</schema>'  
go  
-- Create table.  
CREATE TABLE T( XmlCol xml(SC) )  
-- Insert sample XML instnace  
INSERT INTO T VALUES ('  
<Root xmlns="QNameXSD" xmlns:ns="https://myURI">  
      <ElemQN>ns:someName</ElemQN>  
</Root>')  
go  
-- Verify the insertion  
SELECT * from T  
go  
-- Result  
<Root xmlns="QNameXSD" xmlns:ns="https://myURI">  
  <ElemQN>ns:someName</ElemQN>  
</Root>   
```  
  
 在以下查询中，<`ElemQN`> 元素的值替换为使用**modify （)** xml 数据类型和 XML DML，如所示的替换值的方法。  
  
```  
-- the value.  
UPDATE T   
SET XmlCol.modify('  
  declare default element namespace "QNameXSD";   
  replace value of /Root[1]/ElemQN   
  with expanded-QName("https://myURI", "myLocalName") ')  
go  
-- Verify the result  
SELECT * from T  
go  
```  
  
 结果如下： 请注意，在元素 <`ElemQN`> 的 QName 类型现在具有新值：  
  
```  
<Root xmlns="QNameXSD" xmlns:ns="urn">  
  <ElemQN xmlns:p1="https://myURI">p1:myLocalName</ElemQN>  
</Root>  
```  
  
 以下语句删除了用于示例的对象。  
  
```  
-- Cleanup  
DROP TABLE T  
go  
drop xml schema collection SC  
go  
```  
  
### <a name="b-dealing-with-the-limitations-when-using-the-expanded-qname-function"></a>B. 处理使用 expanded-QName() 函数时的限制。  
 **展开的 QName**函数不能用于 XML 构造。 下面的示例阐释了这一点。 为了消除此限制，该示例首先插入一个节点，然后修改此节点。  
  
```  
-- if exists drop the table T  
--drop table T  
-- go  
-- Create XML schema collection  
-- DROP XML SCHEMA COLLECTION SC  
-- go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" type="QName" nillable="true"/>  
</schema>'  
go  
 -- Create table T with a typed xml column (using the XML schema collection)  
CREATE TABLE T (xmlCol XML(SC))  
go  
-- Insert an XML instance.  
insert into T values ('<root xmlns:a="https://someURI">a:b</root>')  
 go  
-- Verify  
SELECT *   
FROM T  
```  
  
 以下示例尝试添加另一个 <`root`> 元素但未成功，因为 XML 构造中不支持 expanded-qname （） 函数。  
  
```  
update T SET xmlCol.modify('  
insert <root>{expanded-QName("http://ns","someLocalName")}</root> as last into / ')  
go  
```  
  
 此解决方案是首先插入值的实例 <`root`> 元素，然后修改它。 在此示例中，使用初始值为空时 <`root`> 插入元素。 在此示例中的 XML 架构集合允许值为空 <`root`> 元素。  
  
```  
update T SET xmlCol.modify('  
insert <root xsi:nil="true"/> as last into / ')  
go  
-- now replace the nil value with another QName.  
update T SET xmlCol.modify('  
replace value of /root[last()] with expanded-QName("http://ns","someLocalName") ')  
go  
 -- verify   
SELECT * FROM T  
go  
-- result  
<root>b</root>  
```  
  
 `<root xmlns:a="https://someURI">a:b</root>`  
  
 `<root xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:p1="http://ns">p1:someLocalName</root>`  
  
 可以比较 QName 值，如以下查询所示。 查询仅返回 <`root`> 元素的值匹配 QName 类型返回值**expanded-qname （)** 函数。  
  
```  
SELECT xmlCol.query('  
    for $i in /root  
    return  
       if ($i eq expanded-QName("http://ns","someLocalName") ) then  
          $i  
       else  
          ()')  
FROM T  
```  
  
### <a name="implementation-limitations"></a>实现限制  
 还有一个限制：**Expanded-qname （)** 函数接受空序列，第二个参数，并将返回空，而不是第二个参数不正确时引发运行时错误。  
  
## <a name="see-also"></a>请参阅  
 [与 Qname 相关的函数&#40;XQuery&#41;](https://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
