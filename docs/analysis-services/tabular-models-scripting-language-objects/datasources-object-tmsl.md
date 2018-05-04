---
title: 数据源对象 (TMSL) |Microsoft 文档
ms.custom: ''
ms.date: 05/30/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 1357ae7e-30a4-481a-831c-7b046fe15aa4
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2c68188cef82e36c931b299cbd9c68cf18b659de
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="datasources-object-tmsl"></a>数据源对象 (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  到数据源模型期间导入将数据添加到模型，或在传递通过 DirectQuery 模式下的查询，或者使用定义的连接。  在 DirectQuery 模式下的模型只能有一个**数据源**对象。  
  
 除非您要创建的更换，或更改数据的源对象本身，任何在脚本 （如分区脚本） 中引用的数据源必须是现有**数据源**模型中的对象。  
  
## <a name="object-definition"></a>对象定义  
 所有对象都有一组通用的属性，包括名称、 类型、 说明、 一个属性集合和批注。 **数据源**对象还具有以下属性。  
  
 type  
 DataSource 的类型。 目前，唯一有效的值是提供程序 (1)-标准连接字符串。  
  
 connectionString  
 连接字符串按最小方式指定的服务器和数据库，但还可以包括支持外部 RDBMS，如数据提供程序或用户帐户的其他属性。 此值是必需的。 请参阅[SqlConnectionStringBuilder 类](https://msdn.microsoft.com/en-us/library/ms254500\(v=vs.110\).aspx)有关 SQL Server 的详细信息数据库连接字符串属性。  
  
 impersonationMode  
 指定 Analysis Services 是否应模拟的标识请求查询的用户。 此属性是一个数字值，指定要用于模拟的凭据。 枚举值如下：  
  
-   默认值 (1)-服务器使用它认为适合于在其中使用模拟的上下文的模拟方法。  
  
-   ImpersonateAccount (2) 的服务器将使用指定的用户帐户。  
  
-   ImpersonateAnonymous (3) 的服务器将使用匿名用户帐户。  此选项不建议使用，但有时方案中，使用 HTTP 访问的自定义应用程序处理身份验证。  
  
-   ImpersonateCurrentUser (4)-服务器使用作为连接客户端的用户帐户。  
  
-   ImpersonateServiceAccount (5) 的服务器使用服务器作为运行的用户帐户。  
  
-   ImpersonateUnattendedAccount (6) – 服务器使用的无人参与的用户帐户。 这适用于在 SharePoint 环境中运行的 Power Pivot 或表格模型。  
  
 DirectQuery 模式下可以使用 impersonateCurrentuser，如果 Analysis Services 配置为受信任委派，或  
                      如果在 Analysis Services 服务帐户的安全上下文中进行查询请求，impersonateServiceAccount。 请参阅[配置 Analysis Services for Kerberos 约束委派](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md)。  
  
 account  
 用于模拟。 一个 Windows 帐户或数据库帐户已具有的有效登录名的读取权限外部数据库。  
  
 password  
 提供帐户的密码加密的字符串。  
  
 maxConnections  
 到数据源的要开启的并发连接的最大数量。  
  
 隔离  
 使用执行命令时对数据源的隔离的类型。 有效值为 ReadCommitted （1） 或快照 (2)。  
  
 timeout  
 一个整数，以秒为单位对数据源执行的命令中指定的超时。  
  
 提供程序  
 如果未否则指定连接字符串上，则一个可选的字符串，用于标识托管的数据提供程序的名称对关系数据库中，连接上使用。  
  
## <a name="usage"></a>用法  
 **数据源**中使用对象[Alter 命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md)，[创建命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md)， [CreateOrReplace 命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md)，[删除命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md)，[刷新命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md)，和[撰写 MergePartitions 命令&#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/mergepartitions-command-tmsl.md)。  
  
 A**数据源**对象是一个模型的一个属性，但也可以指定为给定模型和数据库之间的一对一映射的数据库对象的属性。  分区基于 SQL 的查询还指定**数据源**，只能使用一套减少的属性。  
  
 在创建时，替换或更改数据源对象，将指定对象定义的所有读写的属性。 省略一个读 / 写属性被视为删除操作。  
  
## <a name="examples"></a>示例  
 **示例 1** -连接到*FoodMart*上命名实例的远程数据库*销售*在网络服务器名为*Server01*。  
  
```  
"dataSources": [  
      {  
        "name": "SqlServer Server01 FoodMart",  
        "connectionString": "Provider=SQLNCLI11;Data Source=Server01\Sales;Initial Catalog=Foodmart;Integrated Security=SSPI;Persist Security Info=false",  
        "impersonationMode": "impersonateServiceAccount",  
      }  
]  
```  
  
## <a name="full-syntax"></a>完整语法  
 下面是一个模型的数据源对象的架构表示形式。  
  
```  
"dataSources": {  
          "type": "array",  
          "items": {  
            "anyOf": [  
              {  
                "description": "ProviderDataSource object of Tabular Object Model (TOM)",  
                "type": "object",  
                "properties": {  
                  "name": {  
                    "type": "string"  
                  },  
                  "description": {  
                    "type": "string"  
                  },  
                  "type": {  
                    "enum": [  
                      "provider"  
                    ]  
                  },  
                  "connectionString": {  
                    "type": "string"  
                  },  
                  "impersonationMode": {  
                    "enum": [  
                      "default",  
                      "impersonateAccount",  
                      "impersonateAnonymous",  
                      "impersonateCurrentUser",  
                      "impersonateServiceAccount",  
                      "impersonateUnattendedAccount"  
                    ]  
                  },  
                  "account": {  
                    "type": "string"  
                  },  
                  "password": {  
                    "type": "string"  
                  },  
                  "maxConnections": {  
                    "type": "integer"  
                  },  
                  "isolation": {  
                    "enum": [  
                      "readCommitted",  
                      "snapshot"  
                    ]  
                  },  
                  "timeout": {  
                    "type": "integer"  
                  },  
                  "provider": {  
                    "type": "string"  
                  },  
                  "annotations": {  
                    "type": "array",  
                    "items": {  
                      "description": "Annotation object of Tabular Object Model (TOM)",  
                      "type": "object",  
                      "properties": {  
                        "name": {  
                          "type": "string"  
                        },  
                        "value": {  
                          "anyOf": [  
                            {  
                              "type": "string"  
                            },  
                            {  
                              "type": "array",  
                              "items": {  
                                "type": "string"  
                              }  
                            }  
                          ]  
                        }  
                      },  
                      "additionalProperties": false  
                    }  
                  }  
                },  
                "additionalProperties": false  
              }  
            ]  
          }  
        },  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [表格模型脚本语言 (TMSL) 参考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [DirectQuery 模式](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [在 Internet 信息服务 & #40; IIS & #41; 上配置对 Analysis Services 的 HTTP 访问8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)  
  
  
