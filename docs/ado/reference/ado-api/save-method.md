---
title: 保存方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Recordset::Save
- _Recordset::raw_Save
helpviewer_keywords:
- Save method [ADO]
ms.assetid: ed3d9678-5c28-4e61-8bb3-7dfb66d99cf5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 55ba7b2fc9e1b6ea0eaeb44989e1bfb64b44d9d4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63315212"
---
# <a name="save-method"></a>Save 方法
将保存[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)文件中或[Stream](../../../ado/reference/ado-api/stream-object-ado.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
recordset.Save Destination, PersistFormat  
```  
  
#### <a name="parameters"></a>Parameters  
 *目标*  
 可选。 一个**Variant** ，表示该文件的完整路径名称其中**记录集**是要保存，或对引用**Stream**对象。  
  
 *PersistFormat*  
 可选。 一个[PersistFormatEnum](../../../ado/reference/ado-api/persistformatenum.md)值，该值指定在其中的格式**记录集**（XML 或 ADTG） 保存。 默认值是**adPersistADTG**。  
  
## <a name="remarks"></a>备注  
 [Save 方法](../../../ado/reference/ado-api/save-method.md)仅在 open 上调用方法**记录集**。 使用[Open 方法 （ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)更高版本的还原方法**记录集**从*目标*。  
  
 如果[筛选器属性](../../../ado/reference/ado-api/filter-property.md)属性实际上是有关**记录集**，然后保存筛选器下可访问的行。 如果**记录集**是分层的则当前子**记录集**和及其子级都得到保存，包括父**记录集**。 如果子级的 Save 方法**记录集**是调用，保存子及其所有子级，但不是父级。  
  
 首次保存**记录集**，也可不指定*目标*。 如果省略*目标*，将使用设置为源属性的值的名称创建一个新的文件**记录集**。  
  
 省略*目标*当您随后调用**保存**后会发生第一次保存或运行时错误。 如果您随后调用**保存**有一个新*目标*，则**记录集**保存到新的目标。 但是，新的目标和原始目标会将打开。  
  
 **保存**不会关闭**记录集**或*目标*，因此可以继续使用**记录集**并保存所做的最新更改。 *目标*保持打开状态，直到**记录集**已关闭。  
  
 出于安全性原因**保存**方法允许仅从由 Microsoft Internet Explorer 执行的脚本的低和自定义安全设置的使用。  
  
 如果**保存**方法时异步调用**记录集**提取、 执行，或更新操作正在进行，然后**保存**将等待，直到异步操作已完成。  
  
 保存记录开头的第一行**记录集**。 当**保存**方法完成后，当前行位置移动到的第一行**记录集**。  
  
 为获得最佳结果，设置[CursorLocation 属性 (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient**与**保存**。 如果您的提供程序不支持所有必要的功能，保存**记录集**对象时，游标服务将提供该功能。  
  
 当**记录集**与一起持久保留**CursorLocation**属性设置为**adUseServer**，为更新功能**记录集**限制。 通常情况下，仅限单个表中的更新、 插入和删除操作允许 （具体取决于提供程序功能）。 [重新同步方法](../../../ado/reference/ado-api/resync-method.md)方法也是在此配置中不可用。  
  
> [!NOTE]
>  正在保存**记录集**与**字段**类型的**adVariant**， **adIDispatch**，或**adIUnknown**是不支持的 ADO，并可能导致不可预知的结果。  
  
 仅筛选条件字符串的形式 (例如订购日期 >"12/31/1999年) 会影响的内容的持久化**记录集**。 筛选器使用的数组创建**书签**或使用中的值[FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md)将不会影响的内容的持久**记录集**。 这些规则适用于**记录集**创建与客户端或服务器端游标。  
  
 因为*目标*参数可接受任何支持的 OLE DB IStream 接口的对象，可以在保存**记录集**直接向 ASP 响应对象。 有关更多详细信息，请参阅**XML 记录集暂留方案**。  
  
 您还可以保存**记录集**到 MSXML DOM 对象的实例的 XML 格式，如所示以下 Visual Basic 代码：  
  
```  
Dim xDOM As New MSXML.DOMDocument  
Dim rsXML As New ADODB.Recordset  
Dim sSQL As String, sConn As String  
  
sSQL = "SELECT customerid, companyname, contactname FROM customers"  
sConn="Provider=Microsoft.Jet.OLEDB.4.0;Data Source=Northwind.mdb"  
rsXML.Open sSQL, sConn  
rsXML.Save xDOM, adPersistXML   'Save Recordset directly into a DOM tree.  
...  
```  
  
> [!NOTE]
>  以 XML 格式保存分层记录集 （数据形状） 时，将应用两个限制。 你不能将保存到 XML 如果分层**记录集**包含挂起的更新，且不能保存参数化分层**记录集**。  
  
 一个**记录集**保存以 XML 格式保存使用 utf-8 格式。 此类文件加载到 ADO Stream 中，Stream 对象不会尝试打开**记录集**从流除非流的字符集属性设置为 utf-8 格式的相应值。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>请参阅  
 [Save 和 Open 方法示例 (VB)](../../../ado/reference/ado-api/save-and-open-methods-example-vb.md)   
 [Save 和 Open 方法示例 （VC + +）](../../../ado/reference/ado-api/save-and-open-methods-example-vc.md)   
 [Open 方法 （ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open 方法 (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [SaveToFile 方法](../../../ado/reference/ado-api/savetofile-method.md)
