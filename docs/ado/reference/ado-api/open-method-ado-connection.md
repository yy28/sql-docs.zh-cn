---
title: Open 方法 （ADO 连接） |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 008ff3dacaa4bf3256429984973608c10a73d43e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47606478"
---
# <a name="open-method-ado-connection"></a>Open 方法（ADO 连接）
将打开与数据源的连接。  
  
## <a name="syntax"></a>语法  
  
```  
  
connection.Open ConnectionString, UserID, Password, Options  
```  
  
#### <a name="parameters"></a>Parameters  
 *ConnectionString*  
 可选。 一个**字符串**值，该值包含连接信息。 请参阅[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)有关有效的设置的详细信息的属性。  
  
 *用户 Id*  
 可选。 一个**字符串**值，该值包含用于建立连接时使用的用户名。  
  
 *密码*  
 可选。 一个**字符串**值，该值包含要建立连接时使用的密码。  
  
 *选项*  
 可选。 一个[ConnectOptionEnum](../../../ado/reference/ado-api/connectoptionenum.md)值，该值确定此方法应返回后 （同步） 或才能建立连接 （以异步方式）。  
  
## <a name="remarks"></a>备注  
 使用**开放**方法[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象建立与数据源的物理连接。 此方法成功完成后，连接处于活动状态并可针对其发出命令并处理结果。  
  
 使用可选*ConnectionString*参数，以指定其中包含一系列的连接字符串*自变量* *= value*语句用分号分隔，或使用 URL 标识的文件或目录资源。 **ConnectionString**属性将自动继承值，该值用于*ConnectionString*参数。 因此，你可以设置**ConnectionString**的属性**连接**对象然后再打开它，或使用*ConnectionString*参数用于设置或重写在当前连接参数**打开**方法调用。  
  
 如果通过用户和密码中的信息这两个*ConnectionString*参数和可选*UserID*并*密码*自变量， *UserID*并*密码*参数将替代中指定的值*ConnectionString*。  
  
 当通过一个打开结束您的运营**连接**，使用[关闭](../../../ado/reference/ado-api/close-method-ado.md)方法来释放任何关联的系统资源。 关闭对象不会删除它从内存;可以更改其属性设置，并使用**打开**方法稍后再打开它。 若要完全消除从内存对象，请将对象变量设置为*Nothing*。  
  
> [!NOTE]
>  **远程数据服务使用情况**客户端上使用时**连接**对象，**打开**方法实际上不会建立到服务器的连接[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)上打开**连接**对象。  
  
> [!NOTE]
>  Url 使用 http 方案将自动调用[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>适用范围  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [Open 和 Close 方法示例 (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Open 和 Close 方法示例 (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Open 和 Close 方法示例 （VC + +）](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Open 方法 （ADO 记录）](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 方法 （ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open 方法 (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [OpenSchema 方法](../../../ado/reference/ado-api/openschema-method.md)
