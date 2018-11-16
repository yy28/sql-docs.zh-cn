---
title: 注册自定义业务对象 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- custom business object in RDS [ADO]
- registering custom business objects in RDS [ADO]
- business objects in RDS [ADO]
ms.assetid: e9032ad8-d14c-42e3-ba13-cb5f00084a79
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 283e623b045e635ef3165b51270c2a257d7856fd
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/12/2018
ms.locfileid: "51559994"
---
# <a name="registering-a-custom-business-object"></a>注册自定义业务对象
若要通过 Web 服务器已成功启动自定义业务对象 （.dll 或.exe），业务对象的 ProgID 必须输入到注册表中此过程所述。 此 RDS 功能通过运行批准的可执行文件来保护你的 Web 服务器的安全性。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
> [!NOTE]
>  有关 MDAC 2.0 和更高版本和 Windows DAC，默认业务对象，[提高](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)，MDAC/Windows DAC 安装期间默认情况下未注册。 但是，如果**提高**注册为可安全执行安装前计算机上执行，注册表项维护用于新安装。  
  
### <a name="to-register-a-custom-business-object"></a>若要注册的自定义业务对象：  
  
1.  单击**启动**，然后单击**运行**。  
  
2.  类型**RegEdit**然后单击**确定**。  
  
3.  在注册表编辑器中，导航到**HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\W3SVC\Parameters\ADCLaunch**注册表项。  
  
4.  选择**ADCLaunch**键，然后从**编辑**菜单上，指向**新建**然后单击**密钥**。  
  
5.  键入您的自定义业务对象的 ProgID，然后单击**Enter**。 将保留**值**条目保留为空。


