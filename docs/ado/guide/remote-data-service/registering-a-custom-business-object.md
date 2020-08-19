---
description: 注册自定义业务对象
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
author: rothja
ms.author: jroth
ms.openlocfilehash: df390d9e02f31913f74b82ed6196bc2442d1591a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452049"
---
# <a name="registering-a-custom-business-object"></a>注册自定义业务对象
若要成功地通过 Web 服务器启动自定义业务对象 () ，必须在注册表中输入业务对象的 ProgID，如本过程中所述。 此 RDS 功能通过仅运行批准可执行文件来保护 Web 服务器的安全性。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件 (参阅 Windows 8 和 [Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416) ，以了解更多详细信息) 。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到 [WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
> [!NOTE]
>  对于 MDAC 2.0 和更高版本以及 Windows DAC，默认的业务对象 [RDSServer （DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)）在 MDAC/Windows DAC 安装期间默认情况下未注册。 但是，如果在安装之前将 **RDSServer** 注册为在计算机上执行的安全，则会保留该注册表项用于新的安装。  
  
### <a name="to-register-a-custom-business-object"></a>注册自定义业务对象：  
  
1.  单击 " **开始** "，然后单击 " **运行**"。  
  
2.  键入 **RegEdit** ，然后单击 **"确定"**。  
  
3.  在注册表编辑器中，导航到 **HKEY_LOCAL_MACHINE \system\currentcontrolset\services\w3svc\parameters\adclaunch** "注册表项。  
  
4.  选择 **ADCLaunch** 项，然后在 " **编辑**" 菜单中，指向 " **新建** "，然后单击 " **项**"。  
  
5.  键入自定义业务对象的 ProgID，并单击 " **Enter**"。 将 **值** 项保留为空。


