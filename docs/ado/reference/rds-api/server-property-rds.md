---
title: 服务器属性 (RDS) |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
f1_keywords:
- RDS::IBindMgr21::Server
helpviewer_keywords:
- Server property [RDS]
ms.assetid: d2727ce7-da9f-4271-ae3c-9334ef477c14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77ad00d9c21a7f7558f8f5cafc66464c1ffc54f7
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2018
ms.locfileid: "51600177"
---
# <a name="server-property-rds"></a>Server 属性 (RDS)
指示 Internet 信息服务 (IIS) 名称和通信协议。  
  
 可以设置**服务器**的对象标记中的设计时属性[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象，或者在运行时中的脚本代码。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
 **HTTP**  
  
 设计时语法  
  
```  
  
<PARAM NAME="Server" VALUE="http:  
//awebsrvr:port  
">  
  
```  
  
 运行时语法  
  
```  
  
DataControl  
.Server="https://  
awebsrvr:port  
"  
  
```  
  
 **HTTPS**  
  
 设计时语法  
  
```  
  
<PARAM NAME="Server" VALUE="https://awebsrvr:port">  
```  
  
 运行时语法  
  
```  
  
DataControl.Server="https://awebsrvr:port"  
```  
  
 **DCOM**  
  
 设计时语法  
  
```  
  
<PARAM NAME="Server" VALUE="  
computername  
">  
  
```  
  
 运行时语法  
  
```  
  
DataControl.Server="computername"  
```  
  
 **进程内**  
  
 设计时语法  
  
```  
  
<PARAM NAME="Server" VALUE="">  
  
```  
  
 运行时语法  
  
```  
  
DataControl.Server=""  
```  
  
## <a name="parameters"></a>Parameters  
 *awebsrvr*或*computername*  
 一个**字符串**值，该值包含 Internet 或 intranet 路径或计算机名称，如果服务器是在远程计算机; 或为空字符串，如果服务器是本地计算机上。  
  
 *port*  
 可选。 用于连接到运行 IIS 的服务器端口。 Internet Explorer 中设置的端口号 (在**视图**菜单上，单击**选项**，然后选择**连接**选项卡) 或在 IIS 中。  
  
 *DataControl*  
 表示的对象变量**rds。DataControl**对象。  
  
## <a name="remarks"></a>备注  
 服务器是位置其中**rds。DataControl**处理请求 （也就是说，查询或更新）。 默认情况下，处理所有请求通过[提高](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)对象， [MSDFMAP。处理程序](../../../ado/guide/remote-data-service/datafactory-customization.md)组件和[MSDFMAP。INI](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)指定服务器上的文件。 请记住，更改服务器，以协调在旧的和新的设置时**MSDFMAP。INI**文件。 不兼容性可能会成功的请求导致无法在另一台服务器上。 如果服务器属性设置为空字符串""，将在本地计算机上使用这些对象。  
  
## <a name="applies-to"></a>适用范围  
 [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>请参阅  
 [服务器属性示例 (VBScript)](../../../ado/reference/rds-api/server-property-example-vbscript.md)   
 [连接属性 (RDS)](../../../ado/reference/rds-api/connect-property-rds.md)   
 [SQL 属性](../../../ado/reference/rds-api/sql-property.md)   
 [SubmitChanges 方法 (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


