---
description: InternetTimeout 属性 (RDS)
title: InternetTimeout 属性 (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- InternetTimeout property [ADO]
ms.assetid: 4d1c8892-4bbc-4e71-bf4b-ba52c0ea9549
author: rothja
ms.author: jroth
ms.openlocfilehash: 9dbc94caa6266ff2f44a07c8792ff8b6287fd61c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438919"
---
# <a name="internettimeout-property-rds"></a>InternetTimeout 属性 (RDS)
指示请求超时前等待的毫秒数。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件 (参阅 Windows 8 和 [Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416) ，以了解更多详细信息) 。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到 [WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回一个 **长整型** 值，该值表示请求超时前等待的毫秒数。  
  
## <a name="remarks"></a>备注  
 此属性仅适用于通过 HTTP 或 HTTPS 协议发送的请求。  
  
 三层环境中的请求可能需要几分钟的时间来执行。 使用此属性为长时间运行的请求指定额外的时间。  
  
## <a name="applies-to"></a>适用于  

:::row:::
    :::column:::
        [DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
    :::column-end:::
    :::column:::
        [DataSpace 对象 (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另请参阅  
 [InternetTimeout 属性示例 (VB) ](../../../ado/reference/rds-api/internettimeout-property-example-vb.md)   
 [InternetTimeout 属性示例 (VC++)](../../../ado/reference/rds-api/internettimeout-property-example-vc.md)   
 

