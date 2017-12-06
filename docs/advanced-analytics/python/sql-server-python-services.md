---
title: "机器学习 Python 服务 |Microsoft 文档"
ms.date: 11/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ba1dea65-40ea-484a-b767-53680c954934
caps.latest.revision: "38"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 665d307f37bca34669de291a2ea0c71d231288a8
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/01/2017
---
# <a name="machine-learning-services-with-python"></a>机器学习服务与 Python

Python 是机器的一种语言提供极大的灵活性和各种不同学习任务的能力。 For Python 开放源代码库包含多个平台的可自定义神经网络，以及用于自然语言处理的常用库。 现在，SQL Server 自 2017 年 1 CTP 2.0 及更高版本支持此广泛使用的语言。

由于与集成 Python[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库引擎，你可以使数据接近的分析并消除成本和与数据移动相关的安全风险。  你可以部署基于 Python 使用便利、 熟悉的工具，例如 Visual Studio 的计算机学习解决方案。 生产应用程序可以获取预测，模型，或从 Python 3.5 运行时通过只需调用 T-SQL 的视觉对象的存储过程。

此版本包括 Python，以及新的 Anaconda 分布[revoscalepy](../python/what-is-revoscalepy.md)库，以提高缩放性和性能机器学习解决方案。

你可以安装所需的一切若要开始使用 Python 通过 SQL Server 2017 安装程序：

+ **机器学习服务 （数据库）：**安装此功能，以及 SQL Server 数据库引擎，若要启用安全执行 Python 脚本在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]计算机。
  
     当你选择了此功能，扩展安装中数据库引擎来支持执行 Python 脚本，以及创建新服务时， [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]、 管理 Python 运行时之间的通信和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。

+ **机器学习 Server （独立版）：**如果不需要 SQL Server 的集成，将获得分布式的机器学习 Python 和 R 支持此功能的安装。 你还可以将你的 Python 解决方案通过使用部署作为 web 服务**mrsdeploy**。
  
     不要在运行 SQL Server 计算机学习 Services 的同一台计算机上安装此功能。


## <a name="additional-resources"></a>其他资源

[设置 Python 机器学习服务数据库中](setup-python-machine-learning-services.md)

[Python 教程](../tutorials/sql-server-python-tutorials.md)
