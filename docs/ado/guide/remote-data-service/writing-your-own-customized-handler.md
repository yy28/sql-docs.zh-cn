---
description: 编写自己的自定义处理程序
title: 编写您自己的自定义处理程序 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 73e71438b7f49472dff8c3f4732c541222598b08
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451839"
---
# <a name="writing-your-own-customized-handler"></a>编写自己的自定义处理程序
如果您是需要默认 RDS 支持的 IIS 服务器管理员，但对用户请求和访问权限有更多控制，则您可能需要编写自己的处理程序。  
  
 MSDFMAP。处理程序实现了 **IDataFactoryHandler** 接口。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件 (参阅 Windows 8 和 [Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416) ，以了解更多详细信息) 。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到 [WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="idatafactoryhandler-interface"></a>IDataFactoryHandler 接口  
 此接口包含两种方法， **dl.getrecordset** 和 **重新连接**。 这两种方法都需要将 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) 属性设置为 **adUseClient**。  
  
 这两个方法均采用 "**Handler =**" 关键字中第一个逗号后出现的参数。 例如， `"Handler=progid,arg1,arg2;"` 将传递的参数字符串 `"arg1,arg2"` ，并 `"Handler=progid"` 将传递 null 参数。  
  
## <a name="getrecordset-method"></a>Dl.getrecordset 方法  
 此方法查询数据源，并使用提供的参数创建新的 [记录集](../../../ado/reference/ado-api/recordset-object-ado.md) 对象。 **记录集**必须用**adLockBatchOptimistic**打开，并且不能异步打开。  
  
### <a name="arguments"></a>参数  
 ***conn***  连接字符串。  
  
 ***args***  处理程序的参数。  
  
 ***查询***  用于进行查询的命令文本。  
  
 ***ppRS***  应在其中返回 **记录集** 的指针。  
  
## <a name="reconnect-method"></a>重新连接方法  
 此方法更新数据源。 它将创建一个新的 [连接](../../../ado/reference/ado-api/connection-object-ado.md) 对象并附加给定的 **记录集**。  
  
### <a name="arguments"></a>参数  
 ***conn***  连接字符串。  
  
 ***args***  处理程序的参数。  
  
 ***pr*** **记录集** 对象。  
  
## <a name="msdfhdlidl"></a>msdfhdl .idl  
 这是出现在**msdfhdl**文件中的**IDataFactoryHandler**的接口定义。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [自定义文件连接部分](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [自定义文件日志部分](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [自定义文件 SQL 部分](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [自定义文件 UserList 部分](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [自定义 DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [必需的客户端设置](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [了解自定义文件](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)


