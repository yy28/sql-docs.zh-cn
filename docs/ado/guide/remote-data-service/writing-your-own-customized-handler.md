---
title: 编写你自己的自定义处理程序 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory handler in RDS [ADO]
- customized handler in RDS [ADO]
ms.assetid: d447712a-e123-47b5-a3a4-5d366cfe8d72
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: daddb9057775e1f098754dd2a331c1dc77194d10
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63155910"
---
# <a name="writing-your-own-customized-handler"></a>编写自己的自定义处理程序
你可能想要编写自己的处理程序，如果您是 IIS 服务器管理员，并且希望获得的默认的 RDS 支持，但更好地控制用户请求和访问权限。  
  
 MSDFMAP。处理程序实现**IDataFactoryHandler**接口。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="idatafactoryhandler-interface"></a>IDataFactoryHandler 接口  
 此接口有两个方法**GetRecordset**并**重新连接**。 这两种方法需要[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient**。  
  
 这两种方法采用中第一个逗号后显示的自变量"**处理程序 =**"关键字。 例如，`"Handler=progid,arg1,arg2;"`将传递的参数字符串，其中`"arg1,arg2"`，和`"Handler=progid"`将传递 null 参数。  
  
## <a name="getrecordset-method"></a>GetRecordset 方法  
 此方法将查询数据源，创建一个新[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象使用提供的参数。 **记录集**必须使用打开**adLockBatchOptimistic** ，必须以异步方式打开。  
  
### <a name="arguments"></a>参数  
 ***conn***连接字符串。  
  
 ***args***处理程序的参数。  
  
 ***查询***进行查询的命令文本。  
  
 ***ppRS***指针位置**记录集**应返回。  
  
## <a name="reconnect-method"></a>重新连接方法  
 此方法更新数据源。 创建一个新[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象并附加给定**记录集**。  
  
### <a name="arguments"></a>参数  
 ***conn***连接字符串。  
  
 ***args***处理程序的参数。  
  
 ***Pr*** A**记录集**对象。  
  
## <a name="msdfhdlidl"></a>msdfhdl.idl  
 这是的接口定义**IDataFactoryHandler**中显示**msdfhdl.idl**文件。  
  
```cpp
[  
  uuid(D80DE8B3-0001-11d1-91E6-00C04FBBBFB3),  
  version(1.0)  
]  
library MSDFHDL  
{  
    importlib("stdole32.tlb");  
    importlib("stdole2.tlb");  
  
    // TLib : Microsoft ActiveX Data Objects 2.0 Library  
    // {00000200-0000-0010-8000-00AA006D2EA4}  
    #ifdef IMPLIB  
    importlib("implib\\x86\\release\\ado\\msado15.dll");  
    #else  
    importlib("msado20.dll");  
    #endif  
  
    [  
      odl,  
      uuid(D80DE8B5-0001-11d1-91E6-00C04FBBBFB3),  
      version(1.0)  
    ]  
    interface IDataFactoryHandler : IUnknown  
    {  
HRESULT _stdcall GetRecordset(  
      [in] BSTR conn,  
      [in] BSTR args,  
      [in] BSTR query,  
      [out, retval] _Recordset **ppRS);  
  
// DataFactory will use the ActiveConnection property  
// on the Recordset after calling Reconnect.  
   HRESULT _stdcall Reconnect(  
      [in] BSTR conn,  
      [in] BSTR args,  
      [in] _Recordset *pRS);  
    };  
};  
```  
  
## <a name="see-also"></a>请参阅  
 [自定义文件 Connect 部分](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [自定义文件 Logs 部分](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [自定义文件 SQL 部分](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [自定义文件 UserList 部分](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [自定义 DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [所需的客户端设置](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [了解自定义文件](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)


