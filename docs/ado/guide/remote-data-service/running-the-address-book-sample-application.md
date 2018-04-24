---
title: 运行通讯簿示例应用程序 |Microsoft 文档
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
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: 3a2644e9-d634-4ae6-a5b7-13fb7b317ec7
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 232a074b9d3e298405d53adb7d5adeaec82ecc66
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="running-the-address-book-sample-application"></a>运行通讯簿示例应用程序
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 若要运行通讯簿应用程序，请按照此过程。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
### <a name="to-run-this-application"></a>若要运行此应用程序  
  
1.  请确保 Microsoft SQL Server 正在运行。 单击**启动**，指向**程序**，指向**Microsoft SQL Server 7.0**，然后单击**Service Manager**。 如果没有在白色圆圈的绿色箭头，然后 SQL Server 正在运行。 如果不是绿色箭头 （白色圆圈内将有红色正方形），单击**开始/继续**。  
  
2.  Microsoft Internet Explorer 4.0 版或更高版本中，键入以下地址：  
  
     **http://** *webserver* **/RDS/AddressBook/AddrBook.asp**  
  
     其中*web 服务器*是 RDS 服务器组件已安装 Web 服务器的名称。  
  
3.  然后，您可以尝试通讯簿示例应用程序，在各种方案，如搜索某个人基于他或她列出"程序管理器"的标题的所有人员的电子邮件名称或编辑现有的记录。 单击**查找**可以用所有可用的姓名填充数据网格。  
  
## <a name="see-also"></a>另请参阅  
 [通讯簿数据绑定对象](../../../ado/guide/remote-data-service/address-book-data-binding-object.md)




