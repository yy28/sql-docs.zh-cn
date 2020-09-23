---
author: MikeRayMSFT
ms.prod: sql
ms.technology: big-data-cluster
ms.topic: include
ms.date: 06/22/2020
ms.author: mikeray
ms.openlocfilehash: b72f8044638adbf75049392fae32447a8a749a6d
ms.sourcegitcommit: d973b520f387b568edf1d637ae37d117e1d4ce32
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85215040"
---
从 SQL Server 2019 CU5 开始，当使用基本身份验证部署新群集时，所有终结点（包括网关）都使用 `AZDATA_USERNAME` 和 `AZDATA_PASSWORD`。 升级到 CU5 的群集上的终结点继续使用 `root` 作为用户名连接到网关终结点。 此更改不适用于使用 Active Directory 身份验证的部署。 请参阅发行说明中的[通过网关终结点访问服务所用的凭据](../big-data-cluster/release-notes-big-data-cluster.md#credentials-for-accessing-services-through-gateway-endpoint)。