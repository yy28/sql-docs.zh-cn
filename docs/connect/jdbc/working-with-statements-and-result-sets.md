---
title: 使用语句和结果集 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cc917534-f5f8-4844-87c8-597c48b4e06d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fb6d545a3a7f8c3b29e5bc372aa4fdadf95edd52
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003785"
---
# <a name="working-with-statements-and-result-sets"></a>使用语句和结果集

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

使用 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 及其提供的 Statement 和 ResultSet 对象时，可使用多种技术来提高应用程序的性能和可靠性。

## <a name="use-the-appropriate-statement-object"></a>使用适当的语句对象

使用 JDBC 驱动程序 Statement 对象时（如 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)、[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 或 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 对象），请确保所使用的对象适用于你的作业。

- 如果没有 OUT 参数, 则无需使用 SQLServerCallableStatement 对象。 改为使用 SQLServerStatement 或 SQLServerPreparedStatement 对象。

- 如果你不想多次执行该语句, 或者不具有 IN 或 OUT 参数, 则无需使用 SQLServerCallableStatement 或 SQLServerPreparedStatement 对象。 相反, 请使用 SQLServerStatement 对象。

## <a name="use-the-appropriate-concurrency-for-resultset-objects"></a>为 ResultSet 对象使用适当的并发

创建生成结果集的语句时，不要请求可更新的并发，除非您的实际意图就是更新这些结果。 对于读取较小的结果集来说，默认的只进、只读游标模型速度最快。

## <a name="limit-the-size-of-your-result-sets"></a>限制结果集的大小

考虑使用 [setMaxRows](../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md) 方法（或 SET ROWCOUNT 或 SELECT TOP N SQL 语法）来限制从可能较大的结果集中返回的行数。 如果必须处理大型结果集，请考虑通过设置连接字符串属性 responseBuffering=adaptive（默认模式）来使用自适应响应缓冲。 此方法使应用程序无需服务器端游标即可处理大型结果集，并最大限度地减少应用程序使用的内存。 有关详细信息, 请参阅[使用自适应缓冲](../../connect/jdbc/using-adaptive-buffering.md)。

## <a name="use-the-appropriate-fetch-size"></a>使用适当的提取大小

对于只读服务器游标，需要权衡的是与服务器之间的往返通信与驱动程序所使用的内存量。 对于可更新的服务器游标，提取大小还会影响结果集对更改的敏感度和服务器上的并发。 在显式调用 [refreshRow](../../connect/jdbc/reference/refreshrow-method-sqlserverresultset.md) 方法或游标离开提取缓冲区之前，当前提取缓冲区中的行更新并不可见。 如果使用 CONCUR_SS_SCROLL_LOCKS (1009)，则较大的提取缓冲区具有较好的性能（较少的服务器往返通信），但具有较低的更改敏感度且服务器上的并发会减少。 若要获得最大的更改敏感度，请将提取大小设为 1。 然而，需要注意的是，这样会导致每提取一行就发生一次服务器往返通信。

## <a name="use-streams-for-large-in-parameters"></a>对较大的 IN 参数使用流

可使用已逐渐具体化的流或 BLOB 和 CLOB，来处理对较大的列值的更新或对较大的 IN 参数的发送。 JDBC 驱动程序通过多次往返通信将其“分块”发送到服务器，这样您便可以设置和更新超出内存允许范围的值。

## <a name="see-also"></a>另请参阅

[借助 JDBC 驱动程序提高性能和可靠性](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)
