---
title: 授予 Web 服务器计算机来宾特权 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- guest privileges in RDS [ADO]
ms.assetid: e851a22d-01bc-4eb0-bc42-92b8f65d1c63
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8f0ebb888b223cab81d01817ec4c10f96813d3f3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47678475"
---
# <a name="granting-guest-privileges-to-a-web-server-computer"></a>授予 Web 服务器计算机来宾特权
匿名的 Web 服务器帐户 (IUSR_*ComputerName*) 必须添加到来宾本地组 Web 服务器计算机上使用 rds。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/en-us/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
### <a name="to-grant-guest-privileges-to-a-web-server-computer"></a>若要授予对 Web 服务器计算机来宾特权  
  
1.  在 Microsoft Windows 2000 Server 计算机上，单击**启动**，依次指向**程序**，指向**管理工具**，然后单击**计算机管理**。  
  
2.  在控制台树中，在**本地用户和组**，单击**组**。  
  
3.  选择**来宾**本地组。 从**操作**菜单中，选择**属性**。  
  
4.  在中**来宾属性**对话框中，单击**添加**。  
  
5.  如果在列表中不显示匿名的 Web 服务器帐户**选择用户或组**对话框框中，键入其名称 (IUSR_*ComputerName*) 到下空白框中，然后单击**添加**.  
  
6.  单击“确定” 。


