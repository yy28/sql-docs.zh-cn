---
title: 使用透明网络 IP 解析 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d255208f-d486-4ad3-8080-61c6e0261825
caps.latest.revision: 2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d76e50b4761e8d1a32bbcfc4606778f96513ed1
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38060224"
---
# <a name="using-transparent-network-ip-resolution"></a>使用透明网络 IP 解析
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

TransparentNetworkIPResolution 是功能的现有 MultiSubnetFailover 提供，Microsoft ODBC Driver 13.1 for SQL Server，影响的主机名的第一个已解析的 IP 却没有这种情况中的驱动程序的连接顺序中的修订版本响应并且没有与主机名相关联的多个 Ip。 它与 MultiSubnetFailover 提供以下三个连接序列进行交互：

* 0： 一个尝试 IP 后, 跟并行中的所有 Ip
* 1： 尝试并行中的所有 Ip
* 2： 所有 Ip 都尝试一个接一个

|transparentNetworkIPResolution|MultiSubnetFailover|行为|
|:-:|:-:|:-:|
|（默认值）|（默认值）|0|
|（默认值）|已启用|@shouldalert|
|（默认值）|禁用|0|
|已启用|（默认值）|0|
|已启用|已启用|@shouldalert|
|已启用|禁用|0|
|禁用|（默认值）|2|
|禁用|已启用|@shouldalert|
|禁用|禁用|2|

`TransparentNetworkIPResolution`连接字符串和 DSN 关键字控制连接字符串级别的此设置。 默认情况下启用。

关键字|值|，则“默认”
-|-|-
`TransparentNetworkIPResolution`|`Yes`、`No`|`Yes`

`SQL_COPT_SS_TNIR`预连接属性允许控制以编程方式设置此应用程序：

连接属性|   大小/类型|  ，则“默认”| ReplTest1| 描述
-|-|-|-|-
`SQL_COPT_SS_TNIR` (1249)| `SQL_IS_INTEGER` 或 `SQL_IS_UINTEGER`| `SQL_IS_ON`(1), `SQL_IS_OFF`(0)|`SQL_IS_ON`|启用或禁用了 TNIR。

<a name="for-more-information-about-multisubnetfailover-see-odbc-driver-on-linux-and-macos---high-availability-and-disaster-recoveryconnectodbclinux-macodbc-driver-on-linux-support-for-high-availability-disaster-recoverymd"></a>MultiSubnetFailover 有关详细信息，请参阅[Linux 和 macOS 的高可用性和灾难恢复的 ODBC 驱动程序](../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)
--------------------------------------------------
## <a name="see-also"></a>另请参阅  
* [Windows 上的 Microsoft ODBC Driver for SQL Server](../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
* [SQL Server 多子网群集 (SQL Server)](https://msdn.microsoft.com/library/ff878716.aspx#RelatedContent)
