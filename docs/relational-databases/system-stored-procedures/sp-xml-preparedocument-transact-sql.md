---
title: sp_xml_preparedocument (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_xml_preparedocument_TSQL
- sp_xml_preparedocument
dev_langs:
- TSQL
helpviewer_keywords:
- sp_xml_preparedocument
ms.assetid: 95f41cff-c52a-4182-8ac6-bf49369d214c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e89ebe73f7bee6f44df353afca515aca4cbbdcf2
ms.sourcegitcommit: f62f70298651d6223fa5d215b6a7a0d2ffecbd0d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/19/2018
ms.locfileid: "51947615"
---
# <a name="spxmlpreparedocument-transact-sql"></a>sp_xml_preparedocument (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  读取作为输入提供的 XML 文本，然后使用 MSXML 分析器 (Msxmlsql.dll) 对其进行分析，并提供分析后的文档供使用。 分析后的文档对 XML 文档中的各节点（元素、属性、文本和注释等）的树状表示形式。  
  
 **sp_xml_preparedocument**返回可用于访问新创建的内部表示形式的 XML 文档的句柄。 此句柄无效，或直到该句柄无效，通过执行的会话的持续时间内**sp_xml_removedocument**。  
  
> [!NOTE]  
>  分析后的文档存储在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的内部缓存中。 MSXML 分析器占用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可用总内存的八分之一。 若要避免内存不足，请运行**sp_xml_removedocument**要释放的内存。  
  
> [!NOTE]  
>  有关向后兼容性**sp_xml_preparedocument**折叠 CR （char(13)) 和 LF （即使这些字符已实体化的特性中 char(10)) 个字符。  
  
> [!NOTE]  
>  通过调用的 XML 分析器**sp_xml_preparedocument**可分析内部 Dtd 和实体声明。 因为恶意构造的 Dtd 和实体声明可用于执行拒绝服务攻击，我们强烈建议用户不能直接传递到不受信任源从 XML 文档**sp_xml_preparedocument**。  
>   
>  为了减少递归实体扩展攻击， **sp_xml_preparedocument**的单个文档的顶层实体下可扩展的实体数限制为 10,000。 该限制不适用于字符或数字实体。 通过该限制，可以存储带有多个实体引用的文档，同时可以禁止在长于 10,000 个扩展的链中递归扩展任意实体。  
  
> [!NOTE]  
>  **sp_xml_preparedocument**限制为 256 一次可以打开的元素数。  

 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_xml_preparedocument  
hdoc   
OUTPUT  
[ , xmltext ]  
[ , xpath_namespaces ]   
```  
  
## <a name="arguments"></a>参数  
 *hdoc*  
 新建文档的句柄。 *hdoc*是一个整数。  
  
 [ *xmltext* ]  
 是原来的 XML 文档。 MSXML 分析器分析该 XML 文档。 *xmltext*是一个文本参数： **char**， **nchar**， **varchar**， **nvarchar**，**文本**， **ntext**或**xml**。 默认值为 NULL，在此情况下将创建一个空 XML 文档的内部表示形式。  
  
> [!NOTE]  
>  **sp_xml_preparedocument**只能处理文本或非类型化的 XML。 如果将作为输入的实例值已经是类型化的 XML，首先将它转换为新的非类型化的 XML 实例，或者转换为一个字符串，然后传递该值作为输入。 有关详细信息，请参阅 [类型化的 XML 与非类型化的 XML 的比较](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)。  
  
 [ *xpath_namespaces* ]  
 指定在 OPENXML 的行和列 XPath 表达式中使用的命名空间声明。 *xpath_namespaces*是一个文本参数： **char**， **nchar**， **varchar**， **nvarchar**，**文本**， **ntext**或**xml**。  
  
 默认值是**\<根 xmlns:mp ="urn： 架构-microsoft-com:xml-metaprop">**。 *xpath_namespaces*通过格式正确的 XML 文档在 OPENXML 中的 XPath 表达式中使用的前缀提供命名空间 Uri。 *xpath_namespaces*声明必须用于引用命名空间的前缀**urn： 架构-microsoft-com:xml-metaprop**; 这提供了有关分析的 XML 元素的元数据。 虽然可以使用这项技术来为元属性命名空间重新定义命名空间前缀，但该命名空间不会丢失。 前缀**mp**仍有效**urn： 架构-microsoft-com:xml-metaprop**即使*xpath_namespaces*包含任何此类声明。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 >0（失败）  
  
## <a name="permissions"></a>权限  
 要求 **公共** 角色具有成员身份。  
  
## <a name="examples"></a>示例  
  
### <a name="a-preparing-an-internal-representation-for-a-well-formed-xml-document"></a>A. 为格式正确的 XML 文档准备内部表示形式  
 以下示例返回作为输入提供的 XML 文档的新建内部表示形式的句柄。 在对 `sp_xml_preparedocument` 的调用中，将使用默认的命名空间前缀映射。  
  
```  
DECLARE @hdoc int;  
DECLARE @doc varchar(1000);  
SET @doc ='  
<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order CustomerID="VINET" EmployeeID="5" OrderDate="1996-07-04T00:00:00">  
      <OrderDetail OrderID="10248" ProductID="11" Quantity="12"/>  
      <OrderDetail OrderID="10248" ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order CustomerID="LILAS" EmployeeID="3" OrderDate="1996-08-16T00:00:00">  
      <OrderDetail OrderID="10283" ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>';  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @hdoc OUTPUT, @doc;  
-- Remove the internal representation.  
exec sp_xml_removedocument @hdoc;  
```  
  
### <a name="b-preparing-an-internal-representation-for-a-well-formed-xml-document-with-a-dtd"></a>B. 为带 DTD 的格式正确的 XML 文档准备内部表示形式  
 以下示例返回作为输入提供的 XML 文档的新建内部表示形式的句柄。 存储过程根据文档中包含的 DTD 来验证装载的文档。 在对 `sp_xml_preparedocument` 的调用中，将使用默认的命名空间前缀映射。  
  
```  
DECLARE @hdoc int;  
DECLARE @doc varchar(2000);  
SET @doc = '  
<?xml version="1.0" encoding="UTF-8" ?>   
<!DOCTYPE root   
[<!ELEMENT root (Customers)*>  
<!ELEMENT Customers EMPTY>  
<!ATTLIST Customers CustomerID CDATA #IMPLIED ContactName CDATA #IMPLIED>]>  
<root>  
<Customers CustomerID="ALFKI" ContactName="Maria Anders"/>  
</root>';  
  
EXEC sp_xml_preparedocument @hdoc OUTPUT, @doc;  
```  
  
### <a name="c-specifying-a-namespace-uri"></a>C. 指定命名空间 URI  
 以下示例返回作为输入提供的 XML 文档的新建内部表示形式的句柄。 在调用`sp_xml_preparedocument`保留`mp`元属性命名空间映射到前缀和添加`xyz`命名空间映射前缀`urn:MyNamespace`。  
  
```  
DECLARE @hdoc int;  
DECLARE @doc varchar(1000);  
SET @doc ='  
<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order CustomerID="VINET" EmployeeID="5"   
           OrderDate="1996-07-04T00:00:00">  
      <OrderDetail OrderID="10248" ProductID="11" Quantity="12"/>  
      <OrderDetail OrderID="10248" ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order CustomerID="LILAS" EmployeeID="3"   
           OrderDate="1996-08-16T00:00:00">  
      <OrderDetail OrderID="10283" ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @hdoc OUTPUT, @doc, '<ROOT xmlns:xyz="urn:MyNamespace"/>';  
```  
  
## <a name="see-also"></a>请参阅  
 <br>[XML 存储 Procedures(Transact-SQL)](../../relational-databases/system-stored-procedures/xml-stored-procedures-transact-sql.md)
 <br>[系统存储 Procedures(Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)
 <br>[OPENXML(Transact-SQL)](../../t-sql/functions/openxml-transact-sql.md)
 <br>[sys.dm_exec_xml_handles (Transact SQL)](../system-dynamic-management-views/sys-dm-exec-xml-handles-transact-sql.md)
 <br>[sp_xml_removedocument (TRANSACT-SQL)](../../relational-databases/system-stored-procedures/sp-xml-removedocument-transact-sql.md)
  
  
