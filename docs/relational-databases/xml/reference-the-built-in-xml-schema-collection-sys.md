---
title: 引用内置 XML 架构集合 (sys) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- sys XML schema collections [SQL Server]
- schema collections [SQL Server], predefined
- predefined XML schema collections [SQL Server]
- XML schema collections [SQL Server], predefined
- built-in XML schema collections [SQL Server]
ms.assetid: 1e118303-5df0-4ee4-bd8d-14ced7544144
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 249b9d920a15e9eb2b3e85532df7df144b9d4c84
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "67995291"
---
# <a name="reference-the-built-in-xml-schema-collection-sys"></a>引用内置 XML 架构集合 (sys)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  创建的每个数据库在 **sys** 关系架构中都有一个预定义的 **sys** XML 架构集合。 数据库将保留这些预定义架构，这些架构可以从任何其他用户创建的 XML 架构集合进行访问。 这些预定义架构中使用的前缀在 XQuery 中是有意义的。 只有 **xml** 是保留前缀。  
  
```  
xml = http://www.w3.org/XML/1998/namespace  
xs = http://www.w3.org/2001/XMLSchema  
xsi = http://www.w3.org/2001/XMLSchema-instance  
fn = http://www.w3.org/2004/07/xpath-functions  
sqltypes = https://schemas.microsoft.com/sqlserver/2004/sqltypes  
xdt = http://www.w3.org/2004/07/xpath-datatypes  
(no prefix) = urn:schemas-microsoft-com:xml-sql  
(no prefix) = https://schemas.microsoft.com/sqlserver/2004/SOAP  
```  
  
 注意， **sqltypes** 命名空间包含可以从任何用户创建的 XML 架构集合引用的组件。 可以从 **Microsoft Web site** 下载 [sqltypes](https://go.microsoft.com/fwlink/?linkid=31850)架构。 内置组件包括：  
  
-   XSD 类型  
  
-   XML 属性 **lang**, **base**和 **space**  
  
-   **sqltypes** 命名空间的组件  
  
 下面的查询将返回可以从用户创建的 XML 架构集合引用的内置组件：  
  
```  
SELECT C.name, N.name, C.symbol_space_desc from sys.xml_schema_components C join sys.xml_schema_namespaces N  
on ((C.xml_namespace_id = N.xml_namespace_id) AND (C.xml_collection_id = N.xml_collection_id))  
join sys.xml_schema_collections SC  
on SC.xml_collection_id = C.xml_collection_id  
where ((C.xml_collection_id = 1) AND (C.name is not null) AND (C.scoping_xml_component_id is null)   
AND (SC.schema_id = 4))  
GO  
```  
  
 以下示例说明如何在用户架构中引用这些组件。 `CREATE XML SCHEMA COLLECTION` 可创建引用在 `varchar` 命名空间中定义的 `sqltypes` 类型的 XML 架构集。 该示例还引用了在 `lang` 命名空间中定义的 `xml` 属性。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema   
   xmlns="http://www.w3.org/2001/XMLSchema"   
   targetNamespace="myNS"  
   xmlns:ns="myNS"  
   xmlns:s="https://schemas.microsoft.com/sqlserver/2004/sqltypes" >   
   <import namespace="http://www.w3.org/XML/1998/namespace"/>  
   <import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
   <element name="root">  
      <complexType>  
          <sequence>  
             <element name="a" type="string"/>  
             <element name="b" type="string"/>  
             <!-- varchar type is defined in the sys.sys collection and   
                  can be referenced in any user-defined schema -->  
             <element name="c" type="s:varchar"/>  
          </sequence>  
          <attribute name="att" type="int"/>  
          <!-- xml:lang attribute is defined in the sys.sys collection   
               and can be referenced in any user-defined schema -->  
          <attribute ref="xml:lang"/>  
      </complexType>  
    </element>  
 </schema>'  
GO  
 -- Cleanup  
DROP xml schema collection SC   
GO  
```  
  
 您应当注意下列问题：  
  
-   您不能在任何用户定义的 XML 架构集合中使用这些命名空间来修改 XML 架构。 例如，由于正在向受保护的命名空间 `sqltypes` 添加组件，下面的 XML 架构集合将失败：  
  
    ```  
    CREATE XML SCHEMA COLLECTION SC AS '  
    <schema xmlns="http://www.w3.org/2001/XMLSchema"   
    targetNamespace    
        ="https://schemas.microsoft.com/sqlserver/2004/sqltypes" >   
          <element name="root" type="string"/>  
    </schema>'  
    GO  
    ```  
  
-   您不能使用 `sys` XML 架构集类型化 `xml` 列、变量或参数。 例如，下面的代码将返回错误：  
  
    ```  
    DECLARE @x xml (sys.sys)  
    ```  
  
-   不支持序列化这些内置架构。 例如，下面的代码将返回错误：  
  
    ```  
    SELECT XML_SCHEMA_NAMESPACE(N'sys',N'sys')  
    GO  
    ```  
  
 下面的代码是另一个示例，其中创建了使用在 `varchar` 命名空间中定义的 `sqltypes` 类型的 XML 架构集。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"   
        targetNamespace="myNS" xmlns:ns="myNS"  
        xmlns:s="https://schemas.microsoft.com/sqlserver/2004/sqltypes">  
   <import     
     namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
      <simpleType name="myType">  
            <restriction base="s:varchar">  
                  <maxLength value="20"/>  
            </restriction>  
      </simpleType>  
      <element name="root" type="ns:myType"/>  
</schema>'  
go  
```  
  
 如下所示，您可以创建类型化的 `XML` 变量，为其分配一个 XML 实例，并验证 <`root`> 元素类型的值是否是 `varchar` 类型。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xmlns="myNS">My data</root>'  
SELECT @var.query('declare namespace sqltypes = "https://schemas.microsoft.com/sqlserver/2004/sqltypes";  
declare namespace ns="myNS";   
data(/ns:root[1]) instance of sqltypes:varchar?')  
GO  
```  
  
 由于 <`instance of sqltypes:varchar?`> 元素值的类型是根据与 `root` 变量关联的架构从 **varchar** 中派生，因此，`@var` 表达式返回 TRUE。  
  
## <a name="see-also"></a>另请参阅  
 [XML 架构集合 (SQL Server)](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
