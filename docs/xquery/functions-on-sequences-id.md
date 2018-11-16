---
title: id 函数 (XQuery) |Microsoft Docs
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
- fn:id function
- id function
ms.assetid: de99fc60-d0ad-4117-a17d-02bdde6512b4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3a2c5164c884f2611267e22d62bc2d83bc8cfac0
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51659696"
---
# <a name="functions-on-sequences---id"></a>基于序列的函数 - id
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回与匹配一个或多个 xs: idref 值中提供的值的 xs: id 值的元素节点的顺序 *$arg*。  
  
## <a name="syntax"></a>语法  
  
```  
  
fn:id($arg as xs:IDREF*) as element()*  
```  
  
## <a name="arguments"></a>参数  
 *$arg*  
 一个或多个 xs:IDREF 值。  
  
## <a name="remarks"></a>备注  
 此函数的结果是 XML 实例中的一组元素（以文档顺序），其中有 xs:ID 值等于候选 xs:IDREF 列表中的一个或多个 xs:IDREF 值。  
  
 如果 xs:IDREF 值不匹配任何元素，则该函数返回空序列。  
  
## <a name="examples"></a>示例  
 本主题提供了一些针对 XML 实例存储在各种中的 XQuery 示例**xml**类型列中的[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]数据库。  
  
### <a name="a-retrieving-elements-based-on-the-idref-attribute-value"></a>A. 基于 IDREF 属性值检索元素  
 下面的示例使用 fn:id 来基于 IDREF manager 属性检索 <`employee`> 元素。 在此示例中，manager 属性是一个 IDREF 类型的属性，eid 属性是一个 ID 类型的属性。  
  
 对于特定的 manager 属性值， **id （)** 函数查找 <`employee`> 元素，其 ID 类型属性值匹配输入的 IDREF 值。 换句话说，对于特定雇员**id （)** 函数返回雇员经理。  
  
 在该示例中执行下列操作：  
  
-   创建一个 XML 架构集合。  
  
-   类型化**xml**使用 XML 架构集合来创建变量。  
  
-   该查询将检索具有 ID 属性值引用的元素**管理器**IDREF 属性的 <`employee`> 元素。  
  
```  
-- If exists, drop the XML schema collection (SC).  
-- drop xml schema collection SC  
-- go  
  
create xml schema collection SC as  
'<schema xmlns="https://www.w3.org/2001/XMLSchema" xmlns:e="emp" targetNamespace="emp">  
            <element name="employees" type="e:EmployeesType"/>  
            <complexType name="EmployeesType">  
                 <sequence>  
                      <element name="employee" type="e:EmployeeType" minOccurs="0" maxOccurs="unbounded" />  
                 </sequence>  
            </complexType>    
  
            <complexType name="EmployeeType">  
                        <attribute name="eid" type="ID" />  
                        <attribute name="name" type="string" />  
                        <attribute name="manager" type="IDREF" />  
            </complexType>         
</schema>'  
go  
```  
  
```  
declare @x xml(SC)  
set @x='<e:employees xmlns:e="emp">  
<employee eid="e1" name="Joe" manager="e10" />  
<employee eid="e2" name="Bob" manager="e10" />  
<employee eid="e10" name="Dave" manager="e10" />  
</e:employees>'  
  
select @x.value(' declare namespace e="emp";   
 (fn:id(e:employees/employee[@name="Joe"]/@manager)/@name)[1]', 'varchar(50)')   
Go  
```  
  
 该查询返回值“Dave”。 这表示 Dave 是 Joe 的经理。  
  
### <a name="b-retrieving-elements-based-on-the-orderlist-idrefs-attribute-value"></a>B. 基于 OrderList IDREFS 属性值检索元素  
 在下面的示例中，<`Customer`> 元素的 OrderList 属性是一个 IDREFS 类型的属性。 它列出特定客户的订单 ID。 对于每个订单 ID，在 <`Customer`> 下都有一个提供订单值的 <`Order`> 元素子级。  
  
 查询表达式 `data(CustOrders:Customers/Customer[1]/@OrderList)[1]` 检索第一个客户的 IDRES 列表中的第一个值。 然后将此值传递给**id （)** 函数。 然后，该函数查找 <`Order`> 元素的 OrderID 属性值匹配的输入**id （)** 函数。  
  
```  
drop xml schema collection SC  
go  
create xml schema collection SC as  
'<schema xmlns="https://www.w3.org/2001/XMLSchema" xmlns:Customers="Customers" targetNamespace="Customers">  
            <element name="Customers" type="Customers:CustomersType"/>  
            <complexType name="CustomersType">  
                        <sequence>  
                            <element name="Customer" type="Customers:CustomerType" minOccurs="0" maxOccurs="unbounded" />  
                        </sequence>  
            </complexType>  
             <complexType name="OrderType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="OrderValue" type="integer" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="OrderID" type="ID" />  
            </complexType>  
  
            <complexType name="CustomerType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="spouse" type="string" minOccurs="0" maxOccurs="unbounded"/>  
                                <element name="Order" type="Customers:OrderType" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="CustomerID" type="string" />  
                <attribute name="OrderList" type="IDREFS" />  
            </complexType>  
 </schema>'  
go  
declare @x xml(SC)  
set @x='<CustOrders:Customers xmlns:CustOrders="Customers">  
                <Customer CustomerID="C1" OrderList="OrderA OrderB"  >  
                              <spouse>Jenny</spouse>  
                                <Order OrderID="OrderA"><OrderValue>11</OrderValue></Order>  
                                <Order OrderID="OrderB"><OrderValue>22</OrderValue></Order>  
  
                </Customer>  
                <Customer CustomerID="C2" OrderList="OrderC OrderD" >  
                                <spouse>John</spouse>  
                                <Order OrderID="OrderC"><OrderValue>33</OrderValue></Order>  
                                <Order OrderID="OrderD"><OrderValue>44</OrderValue></Order>  
  
                        </Customer>  
                <Customer CustomerID="C3"  OrderList="OrderE OrderF" >  
                                <spouse>Jane</spouse>  
                                <Order OrderID="OrderE"><OrderValue>55</OrderValue></Order>  
                                <Order OrderID="OrderF"><OrderValue>55</OrderValue></Order>  
                </Customer>  
                <Customer CustomerID="C4"  OrderList="OrderG"  >  
                                <spouse>Tim</spouse>  
                                <Order OrderID="OrderG"><OrderValue>66</OrderValue></Order>  
                        </Customer>  
                <Customer CustomerID="C5"  >  
                </Customer>  
                <Customer CustomerID="C6" >  
                </Customer>  
                <Customer CustomerID="C7"  >  
                </Customer>  
</CustOrders:Customers>'  
select @x.query('declare namespace CustOrders="Customers";  
  id(data(CustOrders:Customers/Customer[1]/@OrderList)[1])')  
  
-- result  
<Order OrderID="OrderA">  
  <OrderValue>11</OrderValue>  
</Order>  
```  
  
### <a name="implementation-limitations"></a>实现限制  
 限制如下：  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 不支持的两个参数版本**id （)**。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 需要的参数类型**id （)** 为 xs: idref * 的子类型。  
  
## <a name="see-also"></a>请参阅  
 [基于序列的函数](https://msdn.microsoft.com/library/672d2795-53ab-49c2-bf24-bc81a47ecd3f)  
  
  
