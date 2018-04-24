---
title: CreateObject 方法 (RDS) |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- CreateObject method [ADO]
ms.assetid: dec96be6-0b31-4953-9c9a-e962b5afcd18
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 355c56509e8c06b0d687e5d6164cf0e7c4abe93c
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="createobject-method-rds"></a>CreateObject 方法 (RDS)
创建用于目标业务对象的代理，并将指针返回到它。 与业务对象的通信，以通过 Internet 发送请求和数据服务器端存根 （stub） 将代理包和封送处理数据。 对于进程内组件的对象，不使用代理、 提供只需指向对象的指针。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="syntax"></a>语法  
 远程数据服务支持以下协议： HTTP、 HTTPS (安全套接字层的 HTTP)、 DCOM、 和进程内。  
  
|协议|语法|  
|--------------|------------|  
|HTTP|设置对象 = DataSpace.CreateObject ("ProgId"，"http://awebsrvr")|  
|HTTPS|设置对象 = DataSpace.CreateObject ("ProgId"，"https://awebsrvr")|  
|DCOM|Set object = DataSpace.CreateObject("ProgId", "computername")|  
|进程内|Set object = DataSpace.CreateObject("ProgId", "")|  
  
## <a name="parameters"></a>Parameters  
 *对象*  
 计算结果为一个对象，它在指定的类型的对象变量*ProgID*。  
  
 *DataSpace*  
 表示的对象变量[rds.DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)用于创建新对象的实例的对象。  
  
 *ProgID*  
 A**字符串**包含指定实现应用程序的业务规则的服务器端业务对象的编程标识符的值。  
  
 *awebsrvr*或*computername*  
 A**字符串**值，该值表示用于标识 Internet 信息服务 (IIS) Web 服务器创建服务器业务对象的实例所在的 URL。  
  
## <a name="remarks"></a>注释  
 *HTTP 协议*是标准 Web 协议;*HTTPS*是安全的 Web 协议。 使用*DCOM 协议*运行时没有 HTTP 的本地网络。 *进程内*协议是本地的动态链接库 (DLL)，它不使用网络。  
  
## <a name="applies-to"></a>适用范围  
 [DataSpace 对象 (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)  
  
## <a name="see-also"></a>另请参阅  
 [DataFactory 对象、 查询方法和 CreateObject 方法示例 (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)   
 [DataSpace 对象和 CreateObject 方法示例 (VBScript)](../../../ado/reference/rds-api/dataspace-object-and-createobject-method-example-vbscript.md)   
 [CreateRecordset 方法 (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)


