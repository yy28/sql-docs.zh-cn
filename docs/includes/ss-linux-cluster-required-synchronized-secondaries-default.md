---
ms.openlocfilehash: 2dc81d434714e0a13912fa6f14e1194df5e5afe3
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "68215613"
---
> [!NOTE]
> 创建资源并在之后定期更新，Pacemaker 资源代理会根据可用性组的配置自动设置可用性组上的 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 值。 例如，如果可用性组具有三个同步副本，则代理将 `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 设置为 `1`。 有关详细信息和其他配置选项，请参阅[可用性组配置的高可用性和数据保护](../linux/sql-server-linux-availability-group-ha.md)。 