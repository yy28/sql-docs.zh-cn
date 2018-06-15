---
title: 连接到 Microsoft Azure 订阅 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: cca5a270-643f-4677-8802-98464f19f82a
caps.latest.revision: 4
author: dagiro
ms.author: v-dagir
manager: craigg
ms.openlocfilehash: 78be8dddc2a8d2afc4728280a9f0e1cb618b8d3e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32917462"
---
# <a name="connect-to-a-microsoft-azure-subscription"></a>连接到 Microsoft Azure 订阅
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
使用 **连接到 Microsoft 订阅** 向你的 SQL Server 实例注册现有的 Azure Blob 容器。  对话框将在 Azure Blob 容器中创建共享访问签名和存储访问策略，然后创建 SQL Server 凭据。  使用 SQL Server Management Studio 的备份或还原任务时，将出现该对话框，且此操作涉及到 URL 设备。

## <a name="limitation"></a>限制
**连接到 Microsoft 订阅** 只适用于通过服务管理（经典）部署模型创建的 Azure 存储帐户。  关于 Azure 部署模型的详细信息，请参阅 [Azure Resource Manager vs. classic deployment](https://azure.microsoft.com/en-us/documentation/articles/resource-manager-deployment-model/)（Azure 资源管理器与经典部署）。

## <a name="options"></a>“常规”
**登录**     
使用合适的 Azure 帐户登录。

**选择要使用的订阅**      
从下拉列表中选择所需的订阅。

**选择存储帐户**  
从下拉列表中选择所需的存储帐户。

**选择 Blob 容器**   
从下拉列表中选择所需的 Blob 容器。

**共享访问策略过期**   
共享访问策略会在指定日期后过期。  默认过期时间为创建一年后。  根据需要修改。

**已生成共享访问签名**   
RTF 文本框中将显示已生成的共享访问签名。

**创建凭据**   
按钮将生成存储访问策略和共享访问签名，然后创建一个 SQL Server 凭据。
