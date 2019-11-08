---
ms.openlocfilehash: 497a564a10a3d35b33f47222fce8f89fe36bd15e
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73530927"
---
某些操作（包括配置服务器（实例级）设置或手动将数据库添加到可用性组）需要连接到 SQL Server 实例。 某些操作（例如 `sp_configure`、`RESTORE DATABASE` 或属于可用性组的数据库中的任何 DDL 命令）需要连接到 SQL Server 实例。 默认情况下，大数据群集不包含用于连接到实例的终结点。 必须手动公开此终结点。

有关说明，请参阅[连接到主副本上的数据库](../big-data-cluster/deployment-high-availability.md#instance-connect)。