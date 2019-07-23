---
title: 使用透明网络 IP 解析 |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008485"
---
# <a name="using-transparent-network-ip-resolution"></a>使用透明网络 IP 解析
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

TransparentNetworkIPResolution 是 Microsoft ODBC Driver 13.1 for SQL Server 中可用的现有 MultiSubnetFailover 功能的修订版本, 它会影响驱动程序的连接顺序, 以防主机名的第一个已解析的 IP 不响应并且存在多个与主机名关联的 Ip。 它与 MultiSubnetFailover 交互以提供以下三个连接序列:

* 0: 尝试一个 IP, 然后并行使用所有 Ip
* 1: 以并行方式尝试所有 Ip
* 2: 逐个尝试一个 Ip

|TransparentNetworkIPResolution|MultiSubnetFailover|形容词|
|:-:|:-:|:-:|
|（默认值）|（默认值）|0|
|（默认值）|已启用|1|
|（默认值）|禁用|0|
|已启用|（默认值）|0|
|已启用|已启用|1|
|已启用|禁用|0|
|禁用|（默认值）|2|
|禁用|已启用|1|
|禁用|禁用|2|

`TransparentNetworkIPResolution`连接字符串和 DSN 关键字控制连接字符串级别的此设置。 默认值为 "已启用"。

关键字|值|，则“默认”
-|-|-
`TransparentNetworkIPResolution`|`Yes`、`No`|`Yes`

`SQL_COPT_SS_TNIR`预连接属性允许应用程序以编程方式控制此设置:

连接属性|   大小/类型|  ，则“默认”| ReplTest1| 描述
-|-|-|-|-
`SQL_COPT_SS_TNIR` (1249)| `SQL_IS_INTEGER` 或 `SQL_IS_UINTEGER`| `SQL_IS_ON`(1), `SQL_IS_OFF`(0)|`SQL_IS_ON`|启用或禁用 TNIR。

<a name="for-more-information-about-multisubnetfailover-see-odbc-driver-on-linux-and-macos---high-availability-and-disaster-recoveryconnectodbclinux-macodbc-driver-on-linux-support-for-high-availability-disaster-recoverymd"></a>有关 MultiSubnetFailover 的详细信息, 请参阅[Linux 上的 ODBC 驱动程序和 macOS-高可用性和灾难恢复](../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)
--------------------------------------------------
## <a name="see-also"></a>另请参阅  
* [Windows 上的 Microsoft ODBC Driver for SQL Server](../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
* [SQL Server 多子网群集 (SQL Server)](https://msdn.microsoft.com/library/ff878716.aspx#RelatedContent)
