---
title: id 函数 （XQuery） |微软文档
description: 了解如何使用 XQuery id 函数按文档顺序使用提供的 xs：IDREF 值返回 XML 实例中的元素序列。
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
ms.openlocfilehash: 45b7f9f7ee9fa301b10c29fafb663c3a307509d7
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388517"
---
# <a name="functions-on-sequences---id"></a>基于序列的函数 - id
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回具有 xs：ID 值的元素节点序列，该值与 *$arg*中提供的一个或多个 xs：IDREF 值的值匹配。  
  
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
 本主题针对存储在[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]数据库中各种**xml**类型列中的 XML 实例提供了 XQuery 示例。  
  
### <a name="a-retrieving-elements-based-on-the-idref-attribute-value"></a>A. 基于 IDREF 属性值检索元素  
 下面的示例使用 fn：id 检索基于`employee`IDREF 管理器属性<>元素。 在此示例中，manager 属性是一个 IDREF 类型的属性，eid 属性是一个 ID 类型的属性。  
  
 对于特定的管理器属性值 **，id（）** 函数查找 ID`employee`类型属性值与输入 IDREF 值匹配<>元素。 换句话说，对于特定员工 **，id（）** 函数返回员工经理。  
  
 在该示例中执行下列操作：  
  
-   创建一个 XML 架构集合。  
  
-   使用 XML 架构集合创建类型化**xml**变量。  
  
-   查询检索具有由<>`employee`元素**的经理**IDREF 属性引用的 ID 属性值的元素。  
  
```  
-- If exists, drop the XML schema collection (SC).  
-- drop xml schema collection SC  
-- go  
  
create xml schema collection SC as  
'<schema xmlns="http://www.w3.org/2001/XMLSchema" xmlns:e="emp" targetNamespace="emp">  
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
 在下面的示例中，<>`Customer`元素的 OrderList 属性是 IDREFS 类型属性。 它列出特定客户的订单 ID。 对于每个订单 ID，<>提供`Order`订单值的<`Customer`下有一个<>元素子项。  
  
 查询表达式 `data(CustOrders:Customers/Customer[1]/@OrderList)[1]` 检索第一个客户的 IDRES 列表中的第一个值。 然后，此值将传递给**id（）** 函数。 然后，函数查找orderID`Order`属性值与**id（）** 函数匹配的输入>元素<。  
  
```  
drop xml schema collection SC  
go  
create xml schema collection SC as  
'<schema xmlns="http://www.w3.org/2001/XMLSchema" xmlns:Customers="Customers" targetNamespace="Customers">  
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
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]不支持**id（）** 的两参数版本。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]要求**id（）** 的参数类型是 xs：IDREF*的子类型。  
  
## <a name="see-also"></a>另请参阅  
 [序列上的函数](https://msdn.microsoft.com/library/672d2795-53ab-49c2-bf24-bc81a47ecd3f)  
  
  
