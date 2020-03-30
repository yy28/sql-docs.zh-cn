---
title: 使用透明网络 IP 解析 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d255208f-d486-4ad3-8080-61c6e0261825
author: MightyPen
ms.author: genemi
ms.openlocfilehash: df5b0233168c52b4f79cdc6d2d03cd7b72e16046
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "68008485"
---
# <a name="using-transparent-network-ip-resolution"></a>使用透明网络 IP 解析
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

TransparentNetworkIPResolution 是 Microsoft ODBC Driver 13.1 for SQL Server 中提供的现有 MultiSubnetFailover 功能的修订版。如果第一个解析的主机名 IP 未响应，且存在多个与主机名关联的 IP，此功能会影响驱动程序的连接序列。 它与 MultiSubnetFailover 交互，以提供下列三个连接序列：

* 0：先尝试一个 IP，再并行尝试所有 IP
* 1：并行尝试所有 IP
* 2:逐一尝试所有 IP

|TransparentNetworkIPResolution|MultiSubnetFailover|行为|
|:-:|:-:|:-:|
|（默认值）|（默认值）|0|
|（默认值）|已启用|1|
|（默认值）|已禁用|0|
|已启用|（默认值）|0|
|已启用|已启用|1|
|已启用|已禁用|0|
|已禁用|（默认值）|2|
|已禁用|已启用|1|
|已禁用|已禁用|2|

`TransparentNetworkIPResolution` 连接字符串和 DSN 关键字在连接字符串一级控制此设置。 默认是启用的。

关键字|值|默认
-|-|-
`TransparentNetworkIPResolution`|`Yes`、`No`|`Yes`

使用 `SQL_COPT_SS_TNIR` 预连接属性，应用程序以编程方式控制此设置：

连接属性|   大小/类型|  默认| 值| 说明
-|-|-|-|-
`SQL_COPT_SS_TNIR` (1249)| `SQL_IS_INTEGER` 或 `SQL_IS_UINTEGER`| `SQL_IS_ON`(1), `SQL_IS_OFF`(0)|`SQL_IS_ON`|启用或禁用 TNIR。

<a name="for-more-information-about-multisubnetfailover-see-odbc-driver-on-linux-and-macos---high-availability-and-disaster-recovery"></a>若要详细了解 MultiSubnetFailover，请参阅 [Linux 和 macOS 上的 ODBC 驱动程序 - 高可用性和灾难恢复](../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)
--------------------------------------------------
## <a name="see-also"></a>另请参阅  
* [Windows 上的 Microsoft ODBC Driver for SQL Server](../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
* [SQL Server 多子网群集 (SQL Server)](https://msdn.microsoft.com/library/ff878716.aspx#RelatedContent)
