---
title: RDS 对象模型摘要 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS objects [ADO], object model summary
- RDS object model [ADO]
ms.assetid: 909f9af7-31db-4eec-ad52-650ce74dac2f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6c455d816b3ba5a9606d09e3b05e54583e11ca41
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922534"
---
# <a name="rds-object-model-summary"></a>RDS 对象模型摘要
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
|Object|描述|  
|------------|-----------------|  
|[RDS.DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)|此对象包含要获取的服务器代理的方法。 代理可以是默认或自定义服务器程序 （业务对象）。 服务器程序可能会在 Internet、 intranet、 本地网络，调用也是本地的动态链接库。<br /><br /> **DataSpace**对象是可安全执行脚本。|  
|[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|此对象表示的默认服务器程序。 它将执行默认 RDS 数据检索和更新行为。<br /><br /> **DataFactory**对象不是可安全执行脚本。|  
|[RDS.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)|此对象会自动调用**rds。DataSpace**并**提高**对象。<br /><br /> 使用此对象来调用默认 RDS 数据检索或更新行为。<br /><br /> 此对象还提供了可视控件，若要访问返回的方式**记录集**对象。<br /><br /> **DataControl**对象是可安全执行脚本。|  
  
## <a name="see-also"></a>请参阅  
 [RDS 基础知识](../../../ado/guide/remote-data-service/rds-fundamentals.md)   
 [RDS 方案](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 教程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [RDS 使用情况和安全性](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


