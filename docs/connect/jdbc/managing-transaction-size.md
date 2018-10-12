---
title: 管理事务大小 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 82900342-bc80-445f-98a4-468a303aae1e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 22ef6f66c6a0f1685b824c9c89689465c53f4d2d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47810591"
---
# <a name="managing-transaction-size"></a>管理事务大小
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  当您使用事务时，尽可能使事务保持简短是很重要的。 默认模式为自动提交（可以使用 [setAutoCommit](../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md) 方法启用或禁用此模式），它将提交每个操作。 这对于大多数开发人员来说是最易于处理的模式。  
  
 当您使用手动事务时，确保您的代码尽可能快地提交事务。 让事务保持打开状态会阻止其他用户访问数据。 例如，良好的编程惯例可能是在 catch 块中放入一个回滚调用和在 finally 块中放入一个提交调用。 然而，这取决于您的应用程序的设计。  
  
 使事务大小保持较小可以获得更好的并发性能。 例如，如果您启动手动事务并在一个拥有 20,000 行的表中修改 10,000 行，则所有其他用户都将完全无法访问此表中一半的行数据，即使他们只是读取数据也不例外。 将您的修改量降至 2,000 行后，则其他用户可以访问表中 90% 的行数据。  
  
 此外，如果预计您的应用程序会遇到阻止问题并因此需要超时，则确保使用锁定超时设置。 可以使用 [setLockTimeout](../../connect/jdbc/reference/setlocktimeout-method-sqlserverdatasource.md) 方法完成此操作。 锁定超时的默认值为 -1，这意味着它将无限期阻止，同时等待锁定。 您可以将锁定超时设置为 30 秒，这样，如果其他连接进行阻止，则可以使被阻止的连接超时 30 秒。  
  
## <a name="see-also"></a>另请参阅  
 [借助 JDBC 驱动程序提高性能和可靠性](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
