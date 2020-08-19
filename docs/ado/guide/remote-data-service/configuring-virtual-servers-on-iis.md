---
description: 在 IIS 上配置虚拟服务器
title: 在 IIS 上配置虚拟服务器 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- virtual servers in RDS [ADO]
ms.assetid: 2b4786c6-40c4-4ce1-9ad4-03df436e0aff
author: rothja
ms.author: jroth
ms.openlocfilehash: f4e09c5775d87d3339a4965b587828c613ed89fa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452269"
---
# <a name="configuring-virtual-servers-on-iis"></a>在 IIS 上配置虚拟服务器
在 Internet Information Services 4.0 中创建虚拟服务器时，需要执行以下两个额外步骤，以便将虚拟服务器配置为使用 RDS：  
  
1.  在设置服务器时，请选中 "允许执行访问"。  
  
2.  将 msadcs.dll 移到 *vroot*\msadc，其中 *vroot* 是你的虚拟服务器的主目录。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件 (参阅 Windows 8 和 [Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416) ，以了解更多详细信息) 。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到 [WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="see-also"></a>另请参阅  
 [RDS 基础知识](../../../ado/guide/remote-data-service/rds-fundamentals.md)


