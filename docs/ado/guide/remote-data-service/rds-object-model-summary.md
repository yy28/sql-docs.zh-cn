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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67922534"
---
# <a name="rds-object-model-summary"></a>RDS 对象模型摘要
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件（有关详细信息，请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)）。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
|Object|说明|  
|------------|-----------------|  
|[RDS.空间](../../../ado/reference/rds-api/dataspace-object-rds.md)|此对象包含用于获取服务器代理的方法。 代理可能是默认设置或自定义服务器程序（业务对象）。 服务器程序可以在 Internet、intranet、局域网或本地动态链接库上进行调用。<br /><br /> 对于脚本编写，"**空间**" 对象是安全的。|  
|[RDSServer. DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|此对象表示默认服务器程序。 它执行默认的 RDS 数据检索和更新行为。<br /><br /> **DataFactory**对象对于脚本编写是不安全的。|  
|[RDS.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)|此对象可自动调用**RDS。** RDSServer 和**DataFactory**对象。<br /><br /> 使用此对象可调用默认的 RDS 数据检索或更新行为。<br /><br /> 此对象还为视觉对象提供访问返回的**Recordset**对象的方法。<br /><br /> **DataControl**对象可安全地用于脚本编写。|  
  
## <a name="see-also"></a>另请参阅  
 [RDS 基础知识](../../../ado/guide/remote-data-service/rds-fundamentals.md)   
 [RDS 方案](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS 教程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [RDS 使用情况和安全性](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


