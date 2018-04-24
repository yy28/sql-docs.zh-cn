---
title: 地址簿数据绑定对象 |Microsoft 文档
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
helpviewer_keywords:
- RDS scenarios [ADO], data-binding object
- address book application scenario [ADO], data-binding object
ms.assetid: 080c1925-d453-4b89-92ac-c93591490518
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 353e086d8350364a07486eba2334c76b470237db
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="address-book-data-binding-object"></a>通讯簿数据绑定对象
通讯簿应用程序使用[rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)将数据从 SQL Server 数据库绑定到可视对象 （在这种情况下，DHTML 表格中），在应用程序的客户端 HTML 页中的对象。 事件驱动的 VBScript 程序逻辑使用[rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)到：  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
-   查询数据库，将更新发送到数据库，并刷新该数据网格。  
  
-   允许在数据网格中的用户移动到第一个，接下来，以前或最后一条记录。  
  
 下面的代码定义**rds.DataControl**组件：  
  
```  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=DC1 Width=1 Height=1>  
   <PARAM NAME="SERVER" VALUE="http://<%=Request.ServerVariables("SERVER_NAME")%>">  
   <PARAM NAME="CONNECT" VALUE="Provider=sqloledb;  
Initial Catalog=AddrBookDb;Integrated Security=SSPI;">  
</OBJECT>  
```  
  
 对象标记定义**rds.DataControl**组件在程序中。 标记包含两种类型的参数：  
  
-   与一般的对象标记关联的那些。  
  
-   这些特定于**rds.DataControl**对象。  
  
## <a name="generic-object-tag-parameters"></a>一般的对象标记参数  
 下表介绍与对象标记相关联的参数。  
  
|参数|Description|  
|---------------|-----------------|  
|***CLASSID***|一个标识到系统的嵌入对象的类型的唯一、 128 位数字。 此标识符保留在本地计算机的系统注册表中。 (有关的类 Id **rds.DataControl**对象，请参阅[rds.DataControl 对象](../../../ado/reference/rds-api/datacontrol-object-rds.md)。)|  
|***ID***|定义用于在代码中识别它的嵌入对象的文档范围标识符。|  
  
## <a name="rdsdatacontrol-tag-parameters"></a>RDS.DataControl 标记参数  
 下表介绍特定于的参数**rds.DataControl**对象。 (有关完整列表**rds.DataControl**对象参数，以及何时实现它们，请参阅[rds.DataControl 对象](../../../ado/reference/rds-api/datacontrol-object-rds.md)。)  
  
|参数|Description|  
|---------------|-----------------|  
|[服务器](../../../ado/reference/rds-api/server-property-rds.md)|如果你使用的 HTTP，值前面是在服务器计算机的名称`http://`。|  
|[CONNECT](../../../ado/reference/rds-api/connect-property-rds.md)|提供的必要的连接信息**rds.DataControl**以连接到 SQL Server。|  
|[SQL](../../../ado/reference/rds-api/sql-property.md)|设置或返回用于检索查询字符串[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。|  
  
## <a name="see-also"></a>另请参阅  
 [通讯簿命令按钮](../../../ado/guide/remote-data-service/address-book-command-buttons.md)


