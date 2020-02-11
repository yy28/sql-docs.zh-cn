---
title: Open 方法（ADO 连接） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::raw_Open
- Connection15::Open
- _Connection::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: 663defab-5545-4973-9036-24d5882c9737
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 15115313613ea8f86dd2267c6be3c231cab92503
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931934"
---
# <a name="open-method-ado-connection"></a>Open 方法（ADO 连接）
打开与数据源的连接。  
  
## <a name="syntax"></a>语法  
  
```  
  
connection.Open ConnectionString, UserID, Password, Options  
```  
  
#### <a name="parameters"></a>parameters  
 *ConnectionString*  
 可选。 一个包含连接信息的**字符串**值。 有关有效设置的详细信息，请参阅[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)属性。  
  
 *Id*  
 可选。 一个**字符串**值，该值包含建立连接时要使用的用户名。  
  
 *权限*  
 可选。 一个**字符串**值，该值包含建立连接时要使用的密码。  
  
 *选项*  
 可选。 一个[ConnectOptionEnum](../../../ado/reference/ado-api/connectoptionenum.md)值，该值确定此方法是否应在建立连接后（以同步方式）或之前（以异步方式）返回。  
  
## <a name="remarks"></a>备注  
 对[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象使用**Open**方法可建立与数据源的物理连接。 此方法成功完成后，连接将处于活动中，你可以对其发出命令并处理结果。  
  
 使用可选的*ConnectionString*参数指定包含一系列由分号分隔的*参数* *= 值*语句或使用 URL 标识的文件或目录资源的连接字符串。 **Connectionstring**属性会自动继承用于*ConnectionString*参数的值。 因此，您可以在打开连接对象之前设置**连接**对象的**connectionstring**属性，或使用*ConnectionString*参数在**Open**方法调用期间设置或重写当前连接参数。  
  
 如果在*connectionstring*参数和可选*UserID*和*password*参数中同时传递用户和密码信息， *UserID*和*password*参数将覆盖*connectionstring*中指定的值。  
  
 如果已通过打开的**连接**结束操作，请使用[Close](../../../ado/reference/ado-api/close-method-ado.md)方法释放任何关联的系统资源。 关闭对象并不会将其从内存中删除;您可以更改其属性设置，并使用**open**方法稍后再次打开它。 若要从内存中完全消除对象，请将对象变量设置为*Nothing*。  
  
> [!NOTE]
>  **远程数据服务使用情况**当在客户端**连接**对象上使用时， **Open**方法实际上不会建立到服务器的连接，直到在**连接**对象上打开一个[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
> [!NOTE]
>  使用 http 方案的 Url 将自动调用[用于 Internet 发布的 Microsoft OLE DB 提供程序](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>应用于  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [Open 和 Close 方法示例（VB）](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Open 和 Close 方法示例（VBScript）](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [打开和关闭方法示例（VC + +）](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Open 方法（ADO 记录）](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 方法（ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open 方法（ADO 流）](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [OpenSchema 方法](../../../ado/reference/ado-api/openschema-method.md)
