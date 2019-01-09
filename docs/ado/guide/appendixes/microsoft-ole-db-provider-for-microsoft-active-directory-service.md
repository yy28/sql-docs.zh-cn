---
title: Microsoft Active Directory 服务的 Microsoft OLE DB 提供程序 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADSI provider [ADO]
- Active Directory Service Interfaces provider [ADO]
- providers [ADO], OLE DB provider for Active Directory service
- OLE DB provider for Active Directory service [ADO]
ms.assetid: f9e81452-5675-4cfc-9949-cfbd2fe57534
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 25a076118df9f85ff2449c35dc0273db8a499fac
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52538160"
---
# <a name="microsoft-ole-db-provider-for-microsoft-active-directory-service"></a>Microsoft Active Directory 服务的 Microsoft OLE DB 提供程序
Active Directory 服务接口 (ADSI) 访问接口允许 ADO 连接到通过 ADSI 异类目录服务。 这样，ADO 应用程序只读访问权限对 Microsoft Windows NT 4.0 和 Microsoft Windows 2000 目录服务，除了任何符合 LDAP 的目录服务和 Novell 目录服务。 ADSI 本身基于提供程序模型，以便如果没有新的提供程序让访问到另一个目录，ADO 应用程序将能够无缝地访问它。 ADSI 提供程序是自由线程，并支持 Unicode。  
  
## <a name="connection-string-parameters"></a>连接字符串参数  
 若要连接到此提供程序，请设置**提供程序**的参数[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)属性设置为以下：  
  
```vb
ADSDSOObject  
```  
  
 读取[提供程序](../../../ado/reference/ado-api/provider-property-ado.md)属性将返回此字符串的形式。  
  
## <a name="typical-connection-string"></a>典型的连接字符串  
 此提供程序的典型连接字符串如下所示：  
  
```vb
"Provider=ADSDSOObject;User ID=MyUserID;Password=MyPassword;"  
```  
  
 字符串包含以下关键字。  
  
|关键字|Description|  
|-------------|-----------------|  
|**提供程序**|指定 Active Directory 服务的 OLE DB 访问接口。|  
|**用户 ID**|指定用户名称。 如果省略了此关键字，则使用当前登录名。|  
|**密码**|指定用户密码。 如果省略了此关键字。 然后使用当前登录名。|  
  
> [!NOTE]
>  如果您要连接到的数据源提供程序支持 Windows 身份验证，则应指定**Trusted_Connection = yes**或**Integrated Security = SSPI**而不是用户 ID 和密码在连接字符串中的信息。  
  
## <a name="command-text"></a>命令文本  
 通过以下语法中的提供程序识别由四部分组成的命令文本字符串：  
  
```vb
"Root; Filter; Attributes[; Scope]"  
```  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*Root*|指示**ADsPath**对象从其开始搜索 （即，搜索的根）。|  
|*Filter*|指示 RFC 1960 格式中的搜索筛选器。|  
|*属性*|指示要返回的特性的以逗号分隔列表。|  
|*范围*|可选。 一个**字符串**，它指定搜索范围。 可以为以下各项之一：<br /><br /> -基础-搜索基对象 （搜索的根）。<br />-OneLevel-搜索只有一个级别。<br />-子树搜索整个子树。|  
  
 例如：  
  
```vb
"<LDAP://DC=ArcadiaBay,DC=COM>;(objectClass=*);sn, givenName; subtree"  
```  
  
 提供程序还支持 SQL SELECT 命令文本。 例如：  
  
```vb
"SELECT title, telephoneNumber From 'LDAP://DC=Microsoft, DC=COM' WHERE   
objectClass='user' AND objectCategory='Person'"  
```  
  
## <a name="remarks"></a>备注  
 提供程序不接受简单的表名称或存储的过程调用 (例如， [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md)属性将始终为**adCmdText**)。 请参阅命令文本元素的更全面说明 Active Directory 服务接口文档。  
  
## <a name="recordset-behavior"></a>记录集行为  
 下表列出了提供的功能[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)打开使用此提供程序对象。 只有静态游标类型 (**adOpenStatic**) 可用。  
  
 有关详细信息**记录集**您运行的提供程序配置的行为[支持](../../../ado/reference/ado-api/supports-method.md)方法和枚举[属性](../../../ado/reference/ado-api/properties-collection-ado.md)的集合**记录集**以确定是否存在特定于提供程序的动态属性。  
  
 **标准的 ADO 记录集属性的可用性：**  
  
|属性|可用性|  
|--------------|------------------|  
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|读/写|  
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|读/写|  
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|只读|  
|[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|只读|  
|[书签](../../../ado/reference/ado-api/bookmark-property-ado.md)|读/写|  
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|读/写|  
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|始终**adUseServer**|  
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|始终**adOpenStatic**|  
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|始终**adEditNone**|  
|[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|只读|  
|[Filter](../../../ado/reference/ado-api/filter-property.md)|读/写|  
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|读/写|  
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|不可用|  
|[最大记录](../../../ado/reference/ado-api/maxrecords-property-ado.md)|读/写|  
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|只读|  
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|读/写|  
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|只读|  
|[数据源](../../../ado/reference/ado-api/source-property-ado-recordset.md)|读/写|  
|[状态](../../../ado/reference/ado-api/state-property-ado.md)|只读|  
|[“状态”](../../../ado/reference/ado-api/status-property-ado-recordset.md)|只读|  
  
 **标准的 ADO 记录集方法的可用性：**  
  
|方法|可用？|  
|------------|----------------|  
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|否|  
|[取消](../../../ado/reference/ado-api/cancel-method-ado.md)|否|  
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|否|  
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|否|  
|[克隆](../../../ado/reference/ado-api/clone-method-ado.md)|用户帐户控制|  
|[关闭](../../../ado/reference/ado-api/close-method-ado.md)|用户帐户控制|  
|[删除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|否|  
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|用户帐户控制|  
|[“移动”](../../../ado/reference/ado-api/move-method-ado.md)|用户帐户控制|  
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|用户帐户控制|  
|[MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|用户帐户控制|  
|[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|用户帐户控制|  
|[MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|用户帐户控制|  
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)|用户帐户控制|  
|[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)|用户帐户控制|  
|[再次查询](../../../ado/reference/ado-api/requery-method.md)|用户帐户控制|  
|[重新同步](../../../ado/reference/ado-api/resync-method.md)|用户帐户控制|  
|[支持](../../../ado/reference/ado-api/supports-method.md)|用户帐户控制|  
|[Update](../../../ado/reference/ado-api/update-method.md)|否|  
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|否|  
  
 有关 ADSI 和提供程序的具体情况的详细信息，请参阅 Active Directory 服务接口文档或访问 ADSI 网页。  
  
## <a name="see-also"></a>请参阅  
 [CommandType 属性 (ADO)](../../../ado/reference/ado-api/commandtype-property-ado.md)   
 [ConnectionString 属性 (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md)   
 [属性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [提供程序属性 (ADO)](../../../ado/reference/ado-api/provider-property-ado.md)   
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Supports 方法](../../../ado/reference/ado-api/supports-method.md)
