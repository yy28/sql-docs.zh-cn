---
title: "Save 方法 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Recordset::Save
- _Recordset::raw_Save
helpviewer_keywords:
- Save method [ADO]
ms.assetid: ed3d9678-5c28-4e61-8bb3-7dfb66d99cf5
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: edefe1c8d25abd84d5a5f82d7dde8035d82022ee
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="save-method"></a>Save 方法
将保存[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)文件中或[流](../../../ado/reference/ado-api/stream-object-ado.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
recordset.Save Destination, PersistFormat  
```  
  
#### <a name="parameters"></a>Parameters  
 *目标*  
 可选。 A **Variant** ，表示该文件的完整路径名称其中**记录集**保存，或对引用**流**对象。  
  
 *PersistFormat*  
 可选。 A [PersistFormatEnum](../../../ado/reference/ado-api/persistformatenum.md)值，该值指定在其中的格式**记录集**（XML 或 ADTG） 保存。 默认值是**adPersistADTG**。  
  
## <a name="remarks"></a>注释  
 [Save 方法](../../../ado/reference/ado-api/save-method.md)方法只能在 open 上调用**记录集**。 使用[Open 方法 （ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)到更高版本的还原方法**记录集**从*目标*。  
  
 如果[筛选器属性](../../../ado/reference/ado-api/filter-property.md)属性实际上是为**记录集**，然后保存筛选器访问的行。 如果**记录集**是分层的然后当前子**记录集**和其子都得到保存，包括父**记录集**。 如果子 Save 方法**记录集**是调用子及其所有子级都保存，但不是父。  
  
 第一次保存**记录集**，它是可选若要指定*目标*。 如果省略*目标*，将使用设置为的源属性的值的名称创建一个新文件**记录集**。  
  
 省略*目标*当你随后调用**保存**后将会出现第一次保存或运行时错误。 如果您随后调用**保存**用新*目标*、**记录集**保存到新的目标位置。 但是，新的目标和原始目标将将打开。  
  
 **保存**不会关闭**记录集**或*目标*，因此可以继续使用**记录集**并保存最新更改。 *目标*保持打开状态，除非**记录集**已关闭。  
  
 出于安全，**保存**方法允许仅从由 Microsoft Internet Explorer 中执行的脚本的低和自定义安全设置的使用。  
  
 如果**保存**时异步调用方法**记录集**提取、 执行，或更新操作正在进行，然后**保存**将等待，直到异步操作已完成。  
  
 记录保存开头的第一行**记录集**。 当**保存**方法运行完毕后，当前行位置移动到的第一行**记录集**。  
  
 为获得最佳结果，设置[CursorLocation 属性 (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性**adUseClient**与**保存**。 如果你的提供程序不支持所有必要的功能，保存**记录集**对象，则游标服务将提供该功能。  
  
 当**记录集**一起持久化**CursorLocation**属性设置为**adUseServer**，使用的更新功能**记录集**限制。 通常情况下，仅单表更新、 插入和删除允许 （具体取决于提供程序功能）。 [重新同步方法](../../../ado/reference/ado-api/resync-method.md)方法也将在此配置中不可用。  
  
> [!NOTE]
>  保存**记录集**与**字段**类型的**adVariant**， **adIDispatch**，或**adIUnknown**是不支持的 ADO 并可能导致不可预知的结果。  
  
 仅筛选条件字符串的形式 (例如订购日期 >"12/31/1999年) 会影响的持久化内容**记录集**。 筛选器使用的数组创建**书签**或使用从值[FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md)将不会影响的持久内容**记录集**。 这些规则适用于**记录集**创建与客户端或服务器端游标。  
  
 因为*目标*参数可接受任何支持的 OLE DB IStream 接口的对象，可以保存**记录集**直接向 ASP 响应对象。 有关更多详细信息，请参阅**XML 记录集持久化方案**。  
  
 你还可以保存**记录集**到 MSXML DOM 对象的实例的 XML 格式，作为显示在下面的 Visual Basic 代码：  
  
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
>  两个限制时以 XML 格式保存分层记录集 （数据形状）。 你无法将保存到 XML 如果分层**记录集**包含挂起的更新，且不能保存参数化分层**记录集**。  
  
 A**记录集**保存在 XML 格式保存使用 utf-8 格式。 当此类文件加载到 ADO 流中时，流对象不会尝试打开**记录集**从流除非流的字符集属性设置为适当的值为 utf-8 格式。  
  
## <a name="applies-to"></a>适用范围  
  
|||  
|-|-|  
|[记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>另请参阅  
 [保存和打开方法的示例 (VB)](../../../ado/reference/ado-api/save-and-open-methods-example-vb.md)   
 [保存和打开方法的示例 （VC + +）](../../../ado/reference/ado-api/save-and-open-methods-example-vc.md)   
 [Open 方法 （ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open 方法 （ADO 流）](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [SaveToFile 方法](../../../ado/reference/ado-api/savetofile-method.md)

