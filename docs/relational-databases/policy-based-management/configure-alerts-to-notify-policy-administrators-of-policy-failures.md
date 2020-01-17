---
title: 配置警报以通知管理员策略失败情况
description: 了解如何配置警报，以在 SQL Server 未通过策略评估时通知策略管理员。
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, configure alerts
ms.assetid: e8e60159-d5b0-49d5-91f3-af8e9cb994c1
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 1562a1799e442292d61857d4598da69b4c11c70f
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/31/2019
ms.locfileid: "75557809"
---
# <a name="configure-alerts-to-notify-policy-administrators-of-policy-failures"></a>配置警报以通知策略管理员策略失败情况
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在使用三种自动评估模式之一的模式执行基于策略的管理策略时，如果发生违反策略的情况，则会在事件日志中写入消息。 若要在事件日志中写入此消息时得到通知，您可以创建一个警报以检测此消息并执行操作。 该警报应检测下表所示的消息。  
  
|执行模式|消息号|  
|--------------------|--------------------|  
|更改时: 禁止<br /><br /> （如果为自动）|34050|  
|更改时: 禁止<br /><br /> （如果为按需）|34051|  
|按计划|34052|  
|更改时|34053|  
  
 若要设置警报以响应基于策略的管理错误消息，请参阅以下主题：  
  
-   [创建操作员](../../ssms/agent/create-an-operator.md)  
  
-   [使用错误号创建警报](../../ssms/agent/create-an-alert-using-an-error-number.md)  
  
-   [向操作员分配警报](../../ssms/agent/assign-alerts-to-an-operator.md)  
  
## <a name="permissions"></a>权限  
 在按需评估策略时，将会在用户的安全上下文中执行这些策略。 若要写入错误日志，用户必须具有 ALTER TRACE 权限或者是 sysadmin 固定服务器角色的成员。 具有更低权限的用户评估的策略不会写入事件日志，并且不会触发警报。  
  
 自动执行模式是以 sysadmin 角色成员的身份执行的。 这样，策略便可以写入错误日志并引发警报。  
  
## <a name="additional-considerations-about-alerts"></a>有关警报的其他注意事项  
 请注意下面有关警报的其他注意事项：  
  
-   仅为启用的策略引发警报。 由于无法启用 **“按需”** 策略，因此，不会为按需执行的策略引发警报。  
  
-   如果要执行的操作包括发送电子邮件，您必须配置邮件帐户。 建议您使用数据库邮件。 有关如何设置数据库邮件的详细信息，请参阅 [创建数据库邮件帐户](../../relational-databases/database-mail/create-a-database-mail-account.md)。  
  
  
