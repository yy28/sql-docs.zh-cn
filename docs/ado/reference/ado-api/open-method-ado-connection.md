---
title: Open 方法 （ADO 连接） |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::raw_Open
- Connection15::Open
- _Connection::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: 663defab-5545-4973-9036-24d5882c9737
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 252afc6de9b6cf405fba7ae21a191beef2c198e7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="open-method-ado-connection"></a>Open 方法 （ADO 连接）
打开与数据源的连接。  
  
## <a name="syntax"></a>语法  
  
```  
  
connection.Open ConnectionString, UserID, Password, Options  
```  
  
#### <a name="parameters"></a>Parameters  
 *ConnectionString*  
 選擇性。 A**字符串**值，该值包含连接信息。 请参阅[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)有关有效的设置的详细信息的属性。  
  
 *用户 Id*  
 選擇性。 A**字符串**值，该值包含用于建立连接时所使用的用户名。  
  
 *密码*  
 選擇性。 A**字符串**值，该值包含要建立连接时使用的密码。  
  
 *Options*  
 選擇性。 A [ConnectOptionEnum](../../../ado/reference/ado-api/connectoptionenum.md)值，该值确定是否将此方法应返回后 （同步） 或 （异步） 建立连接之前。  
  
## <a name="remarks"></a>注释  
 使用**打开**方法[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象建立到数据源的物理连接。 此方法成功完成后，连接处于活动状态并可以发出对其的命令，还可以处理的结果。  
  
 使用可选*ConnectionString*自变量以指定包含一系列的连接字符串*参数* *= value*语句由分号分隔，或提供一个 URL 标识的文件或目录资源。 **ConnectionString**属性都将自动继承的值用于*ConnectionString*自变量。 因此，你可以设置**ConnectionString**属性**连接**对象然后再打开它，或使用*ConnectionString*参数用于设置或重写在当前连接参数**打开**方法调用。  
  
 如果用户和密码将信息传递两个在*ConnectionString*自变量和可选*UserID*和*密码*自变量， *UserID*和*密码*自变量将重写中指定的值*ConnectionString*。  
  
 当你结束您的操作通过一个打开**连接**，使用[关闭](../../../ado/reference/ado-api/close-method-ado.md)方法释放任何关联系统资源。 关闭对象不会删除它从内存;你可以更改其属性设置，并使用**打开**方法以后再次打开它。 若要完全消除从内存的对象，请将对象变量设置为*执行任何操作*。  
  
> [!NOTE]
>  **远程数据服务使用情况**时在客户端上使用**连接**对象，**打开**方法不会实际建立之前服务器的连接[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)上打开，**连接**对象。  
  
> [!NOTE]
>  Url 使用 http 方案将自动调用[Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)。 有关详细信息，请参阅[绝对和相对 Url](../../../ado/guide/data/absolute-and-relative-urls.md)。  
  
## <a name="applies-to"></a>适用范围  
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [打开和关闭方法的示例 (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [打开和关闭方法的示例 (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [打开和关闭方法的示例 （VC + +）](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Open 方法 （ADO 记录）](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 方法 （ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open 方法 （ADO 流）](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [OpenSchema 方法](../../../ado/reference/ado-api/openschema-method.md)
