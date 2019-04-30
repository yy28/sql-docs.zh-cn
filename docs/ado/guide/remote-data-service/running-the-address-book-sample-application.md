---
title: 运行通讯簿示例应用程序 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: 3a2644e9-d634-4ae6-a5b7-13fb7b317ec7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7a3b973d0c09d272e8960b2d5bf0d2b438260b74
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63191786"
---
# <a name="running-the-address-book-sample-application"></a>运行通讯簿示例应用程序
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 若要运行通讯簿应用程序，请执行此过程。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
### <a name="to-run-this-application"></a>若要运行此应用程序  
  
1.  请确保 Microsoft SQL Server 正在运行。 单击**启动**，依次指向**程序**，指向**Microsoft SQL Server 7.0**，然后单击**Service Manager**。 如果在白色圆圈中出现一个绿色箭头，然后运行 SQL Server。 如果不是 （有将红色正方形的白色圆圈），单击**开始/继续**。  
  
2.  Microsoft Internet Explorer 4.0 或更高版本中，键入以下地址：  
  
     **https://** *webserver* **/RDS/AddressBook/AddrBook.asp**  
  
     其中*web 服务器*安装 RDS 服务器组件的 Web 服务器的名称。  
  
3.  然后可以尝试在通讯簿示例应用程序中的各种方案，如搜索人员根据其列出了标题为"经理"的所有人的电子邮件名称或编辑现有的记录。 单击**查找**数据网格中填充所有可用的名称。  
  
## <a name="see-also"></a>请参阅  
 [通讯簿数据绑定对象](../../../ado/guide/remote-data-service/address-book-data-binding-object.md)




