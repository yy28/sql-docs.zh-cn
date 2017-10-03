---
title: "发布和使用的 Python 代码 |Microsoft 文档"
ms.custom: 
ms.date: 09/29/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: e3c781449a8f7a1b236508cd21b8c00ff175774f
ms.openlocfilehash: 550056f595b881484f3be272b8ae8b2a6d5455af
ms.contentlocale: zh-cn
ms.lasthandoff: 09/30/2017

---

# <a name="publish-and-consume-python-web-services"></a>发布和使用 Python web 服务

通过使用 Microsoft 机器学习 Server 中的操作化功能，可以将一个有效的 Python 解决方案部署到 web 服务。 本主题介绍成功发布，然后运行你的解决方案的步骤。

> [!IMPORTANT]
>
> 所附带机器学习 Server （独立），并使用机器学习 Server 版 9.1.0 中的功能的 Python 版本开发的目标是此示例。
 > 
 > 若要查看的相似示例，利用 Microsoft 机器学习 Server，版本 9.2.0，最新版本中的功能可在机器学习服务器站点上参阅这篇文章：[部署和管理 Python 中的 web 服务](https://docs.microsoft.com/machine-learning-server/operationalize/python/how-to-deploy-manage-web-services)。

本文的目标受众是数据科学家提供想要了解如何将 Python 代码或模型发布作为在 Microsoft 机器学习 Server 中托管的 web 服务。 本文还说明了如何应用程序可以使用代码或模型。 本文假定您已精通 Python。

**适用于： SQL Server 自 2017 年中的计算机学习 Server （独立）**

## <a name="overview-of-workflow"></a>工作流的概述

从发布到使用 Python web 服务的工作流可以汇总为如下：

1. 满足[先决条件](#prereq)的核心 API Swagger 文档从生成的 Python 客户端库。
2. 将身份验证和标头逻辑添加到你的 Python 脚本。
3. 创建 Python 会话、 准备环境，以及创建要保留环境快照。
4. 发布 web 服务，并将嵌入此快照。
5. 尝试通过使用在你的会话中的 web 服务。
6. 管理这些服务。

![Swagger 工作流](./media/data-scientist-python-workflow.png)

本文讨论的工作流中，每个步骤，并包括使用 iris 数据集的示例 Python 代码。

## <a name="sample-code"></a>示例代码

此代码示例假定你已经满足[先决条件](#prereq)若要从该 Swagger 生成 Python 客户端库使用文件和你已 Autorest。

在代码块中之后, 你将在过程中找到更多详细说明每个 steo 的分步演练。

> [!IMPORTANT]
> 此示例使用本地`admin`帐户进行身份验证。 但是，你应将凭据和[身份验证方法](#python-auth)由管理员配置。

```python
##################################################
##       IMPORT GENERATED CLIENT LIBRARY        ##
##################################################

# Import the generated client library. 
import deployrclient

##################################################
##              AUTHENTICATION                  ##
##################################################

#Using client library generated from Autorest
#Create client instance and point it at an R Server. 
#In this case, R Server is local.
client = deployrclient.DeployRClient("http://localhost:12800")

#Define the login request and provide credentials 
#Update values with the connection parameters from your admin
login_request = deployrclient.models.LoginRequest("<<your-username>>","<<your-password>>")

#Make a call to the /login API. 
#Store the returned an access token in a variable.
token_response = client.login(login_request)

#Add the returned access token to the headers variable.
headers = {"Authorization": "Bearer {0}".format(token_response.access_token)}

#Verify that the server is running.
#Remember to include `headers` in every request!
status_response = client.status(headers) 
print(status_response.status_code)


##################################################
##        CREATE SESSION, MODEL, SNAPSHOT       ##
##################################################

#Since already logged in, create a Python session.
#Define session using name (`Session 1`) and `runtime_type="Python"`.
#Remember to specify the Python runtime type.
create_session_request = deployrclient.models.CreateSessionRequest("Session 1", runtime_type="Python")

#Make the call to start the session. 
#Remember to include headers in every method call to the server.
#Returns a session ID.
response = client.create_session(create_session_request, headers) 
   
#Store the session ID in a variable called `session_id` 
#to be able to identify it later at execution time.
session_id = response.session_id

#Create model - Import SVM and datasets from the SciKit-Learn library
execute_request = deployrclient.models.ExecuteRequest("from sklearn import svm\nfrom sklearn import datasets")
execute_response = client.execute_code(session_id,execute_request, headers)
#Report if it was a success
execute_response.success
   
#Define the untrained Support Vector Classifier (SVC) object
#and the dataset to be preloaded.
execute_request = deployrclient.models.ExecuteRequest("clf=svm.SVC()\niris=datasets.load_iris()\nnames={0:'I. setosa',1:'I. versicolor',2:'I. virginica'}")
#Now, go create the object and preload Iris Dataset in R Server
execute_response = client.execute_code(session_id,execute_request, headers)
#Report if it was a success
execute_response.success
   
#Define two rows from the Iris Dataset as a sample for scoring
workspace_object = deployrclient.models.WorkspaceObject("species_1",[7,3.2,4.7,1.4])
workspace_object_2 = deployrclient.models.WorkspaceObject("species_2",[3,2.6,3,2.5])

#Define how to train the classifier model; what to predict; what to return
execute_request = deployrclient.models.ExecuteRequest(
    "clf.fit(iris.data, iris.target)\n"+
    "result=clf.predict(species_1)\n"+
    "other_result=clf.predict(species_2)",
    [workspace_object,workspace_object_2], #Input
    ["result", "other_result"]) #Output

#Now, go train that model on the Iris Dataset in R Server
execute_response = client.execute_code(session_id,execute_request, headers)

#If successful, print name and result of each output parameter. Else, print error.
if(execute_response.success):
    for result in execute_response.output_parameters:
        print("{0}: {1}".format(result.name,result.value))
else:
    print (execute_response.error_message)

#Create a snapshot of the current session
response = client.create_snapshot(session_id, deployrclient.models.CreateSnapshotRequest("Iris Snapshot"), headers)
#Return the snapshot ID for reference when you publish later.
response.snapshot_id
#If you forget the ID, list every snapshot to get the ID again.
for snapshot in client.list_snapshots(headers):
    print(snapshot)

##################################################
##        PUBLISH AS A SERVICE IN PYTHON        ##
##################################################

#Define a web service that determines the iris species by scoring 
#a vector of sepal length and width, petal length and width

#Set `flower_data` for the sepal and petal length and width
flower_data = deployrclient.models.ParameterDefinition(name = "flower_data", type = "vector")
#Set `iris_species` for the species of iris
iris_species = deployrclient.models.ParameterDefinition(name = "iris_species", type = "vector")

#Define the publish request for the web service and its arguments.
#Specify the code, inputs, outputs, and snapshot.
#Don't forget to set runtime_type="Python"`.
publish_request = deployrclient.models.PublishWebServiceRequest(
       code = "iris_species = [names[x] for x in clf.predict(flower_data)]", 
       input_parameter_definitions = [flower_data], 
       output_parameter_definitions = [iris_species],
       runtime_type = "Python",
       snapshot_id = response.snapshot_id)

#Publish the service using the specified name (iris), version (V1.0)
client.publish_web_service_version("Iris", "V1.0", publish_request, headers)

##################################################
##           CONSUME SERVICE IN PYTHON          ##
##################################################

# Inspect holdings and metadata for service Iris V1.0.
for service in client.get_web_service_version("Iris","V1.0", headers):
    #print service metadata (description, who published,...)
    print(service)
    #Print input and output parameters as defined in service definition object
    print("Input Parameters: {0}".format([str(parameter) for parameter in service.input_parameter_definitions]))
    print("Output Parameters: {0}".format([str(parameter) for parameter in service.output_parameter_definitions]))

#Import the requests library to make requests on the server
import requests
#Import the JSON library to use for pretty printing of json responses
import json

#Create a requests `Session` object.
s = requests.Session()

#Record the R Server endpoint URL hosting the web services you created before
url = "http://localhost:12800"

#Give the request.Session object the authentication headers 
#so you don't have to repeat it with each request.
s.headers = headers

#Retrieve the service-specific swagger file using the requests library.
swagger_resp = s.get(url+"/api/Iris/V1.0/swagger.json")

#Either, download service-specific swagger file using the json library.
with open('iris_swagger.json','w') as f:
   (json.dump(client.get_web_service_swagger("Iris","V1.0",headers),f, indent = 1))

#Or, print just what you need from the Swagger file, 
#such as the routing paths for the endpoints to be consumed.
print(json.dumps(swagger_resp.json()["paths"], indent = 1, sort_keys = True))

#Or, print input and output parameters as defined in the Swagger.io format
print("Input")
print(json.dumps(swagger_resp.json()["definitions"]["InputParameters"], indent = 1, sort_keys = True))
print("Output")
print(json.dumps(swagger_resp.json()["definitions"]["WebServiceResult"], indent = 1, sort_keys = True))

#Make the request to consume the service using these flower_data inputs
resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[7,3.2,4.7,1.4]})
#Print the output
print(json.dumps(resp.json(), indent = 1, sort_keys = True))

#Use input from another Iris species.
resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[3,2.6,3,2.5]})
print(json.dumps(resp.json(), indent = 1, sort_keys = True))

#Use input from another Iris species.
resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[5.1,3.5,1.4,.2]})
print(json.dumps(resp.json(), indent = 1, sort_keys = True))

##################################################
##          MANAGE SERVICES IN PYTHON           ##
##################################################

#Define what needs to be updated. Here we add a description.
#Be sure to specify the runtime_type again.
update_request = deployrclient.models.PublishWebServiceRequest(
    description = "Determines iris species using length and width of sepal and petal", runtime_type = "Python")
#Now update it by specifying the service name and version number
client.patch_web_service_version("Iris", "V1.0", update_request, headers)

#Or, publish another version of the web service, but this time 
#the service returns the species as a string instead of list of strings.
flower_data = deployrclient.models.ParameterDefinition(name = "flower_data", type = "vector")
iris_species = deployrclient.models.ParameterDefinition(name = "iris_species", type = "string")
 
#Define the publish request for the service and its arguments.
#Specify the changed code, inputs, outputs, and snapshot.
#Don't forget to set runtime_type="Python"`.
publish_request = deployrclient.models.PublishWebServiceRequest(
    code = "iris_species = [names[x] for x in clf.predict(flower_data)][0]",
    description = "Determines the species of iris, based on Sepal Length, Sepal Width, Petal Length and Petal Width",
    input_parameter_definitions = [flower_data],
    output_parameter_definitions = [iris_species],
    runtime_type = "Python",
    snapshot_id = response.snapshot_id)
 
#Now, publish the service with version (V2.0)
client.publish_web_service_version("Iris", "V2.0", publish_request, headers)
 
#Make request to consume service using these flower_data inputs; print output
resp = s.post(url+"/api/Iris/V2.0",json={"flower_data":[5.1,3.5,1.4,.2]})
print(json.dumps(resp.json(), indent = 1, sort_keys = True))

#Return the list of all existing web services.
for service in client.get_all_web_services(headers):
    #print the service information
    print(service)
    #Print each input and output parameter
    print("Input Parameters: {0}".format([str(parameter) for parameter in service.input_parameter_definitions]))
    print("Output Parameters: {0}".format([str(parameter) for parameter in service.output_parameter_definitions]))

#Delete the second version we just published.
client.delete_web_service_version("Iris","V2.0",headers)
```

## <a name="walkthrough"></a>演练

本部分介绍代码如何运行更多详细信息。


### <a name="prereq"></a>步骤 1。 创建库的先决条件的客户端

在可以开始发布你 Python 代码和模型 thorugh Microsoft 机器学习服务器之前，必须生成一个客户端库使用对于此版本提供的 Swagger 文档。

1. 在本地计算机上安装 Swagger 代码生成器，并自行熟悉它。 将用于在 Python 中生成的 API 客户端库。 常用工具包括[Azure AutoRest](https://github.com/Azure/autorest) （需要 Node.js） 和[Swagger Codegen](https://github.com/swagger-api/swagger-codegen)。 

2. 下载包含你的机器学习 Server 版本的核心 Api 的 Swagger 文件。 此文件包含一个 Swagger 模板来定义 REST 资源和可以对这些资源调用的操作的列表。 你可以找到此文件在下的`https://microsoft.github.io/deployr-api-docs/swagger/<version>/rserver-swagger-<version>.json`，其中`<version>`是 3 位 R Server 版本号。 

   例如，对于 R Server 9.1 你将从下载： https://microsoft.github.io/deployr-api-docs/9.1.0/swagger/rserver-swagger-9.1.0.json

3. 通过将传递生成静态生成的客户端库`rserver-swagger-<version>.json`文件 Swagger 代码生成器和指定的语言所需。 在这种情况下，应指定 Python。  

   例如，如果你使用 AutoRest 生成 Python 客户端库，它可能如下所示，其中 3 位数字表示 R Server 版本号：
   
   `AutoRest.exe -Input rserver-swagger-9.1.0.json -CodeGenerator Python  -OutputDirectory C:\Users\rserver-user\Documents\Python`
   

   您现在可以提供某些自定义标头并进行其他更改，然后使用生成的客户端库存根 （stub）。 请参阅[命令行界面](https://github.com/Azure/autorest/blob/master/docs/user/cli.md)文档在 GitHub 上以不同的配置选项和首选项，例如重命名命名空间有关的详细信息。
   
4. 了解核心客户端库，以查看你可以进行的各种 API 调用。 

   在本示例中，Autorest 生成某些目录和文件以便 Python 客户端库在您的本地系统上。 默认情况下，命名空间 （和目录） 是`deployrclient`和可能如下所示：
   
   ![Autorest 输出路径](./media/data-scientist-python-autorest.png)

   对于此默认命名空间中，在客户端库自身称为`deploy_rclient.py`。 如果在如 Visual Studio IDE 中打开此文件，你将看到类似如下内容：
   
   ![Python 客户端库](./media/data-scientist-python-client-library.png)



### <a name="step-2-add-authentication-and-header-logic"></a>步骤 2. 添加身份验证和标头的逻辑

请记住，所有 Api 都需要身份验证;因此，所有用户必须时进行身份都验证进行 API 调用使用`POST /login`API 或通过 Azure Active Directory (AAD)。 

若要简化此过程，以便用户无需为每个单个调用提供其凭据，则颁发持有者访问令牌。  此持有者令牌是一种轻型安全令牌，授予对受保护资源的"持有者"访问权限： 在此情况下，机器学习服务器的 Api。 用户已经过身份验证后，应用程序必须验证用户的持有者令牌，以确保身份验证是成功完成，目标方。 若要了解有关管理这些令牌的详细信息，请参阅[安全访问令牌](https://msdn.microsoft.com/microsoft-r/operationalize/security-access-tokens)。

与核心 Api 交互前，先进行身份验证，获取持有者访问权限令牌使用[身份验证方法](https://msdn.microsoft.com/microsoft-r/operationalize/security-authentication)由你的管理员配置，然后将其包括在为每个后续请求的每个标头：

1. 通过导入客户端库，以使其能够通过你首选的 Python 代码编辑器，如 Jupyter、 Visual Studio、 VS Code 中，或 iPython 开始。

   指定客户端库的父目录。 在本示例中，Autorest 生成的客户端库是在`C:\Users\rserver-user\Documents\Python\deployrclient`:

   ```python
   # Import the generated client library
   import deployrclient
   ```

2. 将身份验证逻辑添加到你的应用程序，可以定义从本地计算机到计算机学习服务器的连接、 提供凭据，将捕获访问令牌，将该令牌添加到标头，使用该标头中的所有后续请求。  使用由管理员定义的身份验证方法： 基本的管理员帐户、 Active Directory/LDAP (AD/LDAP) 或 Azure Active Directory (AAD)。

   **AD/LDAP 或`admin`帐户身份验证**

   必须调用`POST /login`为了进行身份验证的 API。 你将需要传入`username`和`password`本地管理员，或如果启用了 Active Directory，将传递 LDAP 帐户信息。 反过来，机学习服务器将颁发的持有者/访问权限令牌。 身份验证后，用户将不需要再次提供凭据，只要令牌仍然有效，并且使用每个请求提交标头。 如果不知道您的连接设置，请联系您的管理员联系。

   ```python
   #Using client library generated from Autorest
   #Create client instance and point it at an R Server. 
   #In this case, R Server is local.
   client = deployrclient.DeployRClient("http://localhost:12800")
   
   #Define the login request and provide credentials. 
   #Update values with the connection parameters from your admin.
   login_request = deployrclient.models.LoginRequest("<<your-username>>","<<your-password>>")
   #Make a call to the /login API. 
   #Store the returned an access token in a variable.
   token_response = client.login(login_request)
   ```

   **Azure Active Directory (AAD) 身份验证**

   你必须通过 AAD 凭据、 授权和客户端 id。 反过来，AAD 将颁发[持有者访问令牌](https://msdn.microsoft.com/microsoft-r/operationalize/security-access-tokens)。 身份验证后，用户将不需要再次提供凭据，只要令牌仍然有效，并且使用每个请求提交标头。 如果不知道您的连接设置，请联系您的管理员联系。

   ```python
   #Import the AAD authentication library
   import adal
   
   #Define the login request and provide credentials. 
   #Use the AAD connection parameters provided by your admin.
   url = "http://localhost:12800"
   authuri = https://login.windows.net,
   tenantid = "<<AAD_DOMAIN>>", 
   clientid = "<<NATIVE_APP_CLIENT_ID>>", 
   resource = "<<WEB_APP_CLIENT_ID>>", 
   
   #Acquire authentication token using AAD Device Code Login
   context = adal.AuthenticationContext(authuri+'/'+tenantid, api_version=None)
   code = context.acquire_user_code(resource, clientid)
   print(code['message'])
   token = context.acquire_token_with_device_code(resource, code, clientid)
   #The authentication code returned must be entered at https://aka.ms/devicelogin 
   ```     

3. 添加`Bearer`访问令牌和机器学习服务器当前正在运行的检查。  此令牌返回在身份验证期间和**必须包括在每个后续请求标头**。 此示例使用由 Autorest 生成一个客户端库。

   > [!IMPORTANT]
   > 每个 API 调用必须进行身份验证。 因此，请记住包括标头包含到每个单个请求的令牌。

   ```python
   #Add the returned access token to the headers variable.
   headers = {"Authorization": "Bearer {0}".format(token_response.access_token)}
   
   #Verify that the server is running.
   #Remember to include `headers` in every request!
   status_response = client.status(headers) 
   print(status_response.status_code)
   ```

### <a name="step-3-prepare-session-and-code"></a>步骤 3. 准备会话和代码

身份验证后，你可以启动 Python 会话，并创建要发布更高版本的模型。 你可以在 web 服务包含任何 Python 代码或模型。 一旦你已设置你的会话环境，你可以甚至将其保存为快照以便可以重新加载您的会话，因为已过。 

> [!IMPORTANT]
> 请记住包括`headers`中的每个请求。

1. R 服务器上创建 Python 会话。 你必须指定名称和 Python 语言 (`runtime_type="Python"`)。  如果不将运行时类型设为 Python，则默认为。

   这是示例的使用由 Autorest 生成的客户端库的延续：

   ```python
   #Since already logged in, create a Python session.
   #Define session using name (`Session 1`) and `runtime_type="Python"`.
   #Remember to specify the Python runtime type.
   create_session_request = deployrclient.models.CreateSessionRequest("Session 1", runtime_type="Python")
   
   #Make the call to start the session. 
   #Remember to include headers in every method call to the server.
   #Returns a session ID.
   response = client.create_session(create_session_request, headers) 
   
   #Store the session ID in a variable called `session_id` 
   #to be able to identify it later at execution time.
   session_id = response.session_id
   ```

2. 创建或调用一个模型中将作为 web 服务发布的 Python

   在此示例中，我们训练机器学习服务器的远程实例上对 Iris 数据集的 SciKit 了解支持向量机 (SVM) 模型。  此数据集是可从[scikit-了解站点](http://scikit-learn.org/stable/auto_examples/datasets/plot_iris_dataset.html)。

   ```python
   #Import SVM and datasets from the SciKit-Learn library
   execute_request = deployrclient.models.ExecuteRequest("from sklearn import svm\nfrom sklearn import datasets")
   execute_response = client.execute_code(session_id,execute_request, headers)
   #Report if it was a success
   execute_response.success
   
   #Define the untrained Support Vector Classifier (SVC) object
   #and the dataset to be preloaded.
   execute_request = deployrclient.models.ExecuteRequest("clf=svm.SVC()\niris=datasets.load_iris()\nnames={0:'I. setosa',1:'I. versicolor',2:'I. virginica'}")
   #Now, go create the object and preload Iris Dataset in R Server
   execute_response = client.execute_code(session_id,execute_request, headers)
   #Report if it was a success
   execute_response.success
   
   #Define two rows from the Iris Dataset as a sample for scoring
   workspace_object = deployrclient.models.WorkspaceObject("species_1",[7,3.2,4.7,1.4])
   workspace_object_2 = deployrclient.models.WorkspaceObject("species_2",[3,2.6,3,2.5])

   #Define how to train the classifier model; what to predict; what to return
   execute_request = deployrclient.models.ExecuteRequest(
       "clf.fit(iris.data, iris.target)\n"+
       "result=clf.predict(species_1)\n"+
       "other_result=clf.predict(species_2)",
       [workspace_object,workspace_object_2], #Input
       ["result", "other_result"]) #Output

   #Now, go train that model on the Iris Dataset in R Server
   execute_response = client.execute_code(session_id,execute_request, headers)

   #If successful, print name and result of each output parameter. Else, print error.
   if(execute_response.success):
       for result in execute_response.output_parameters:
           print("{0}: {1}".format(result.name,result.value))
   else:
       print (execute_response.error_message)
   ```

3. 创建快照的此 Python 会话，因此可以保存在 web 服务和在重现此环境占用的时间。 当你需要包括某些库、 对象、 模型、 文件和项目的已准备好的环境时，快照将非常有用。 快照保存整个工作区和工作目录。 但是，在发布时，你可以使用已创建的快照。

   > [!NOTE] 
   > 尽管在发布 web 服务为环境依赖关系时，还可以使用快照，它可能会带来的消耗时间的性能影响。  为了获得最佳性能，请仔细考虑快照的大小，并确保保留那些工作区对象需要和清除其余部分。 在会话中，你可以使用 Python`del`函数或[ `deleteWorkspaceObject` API 请求](https://microsoft.github.io/deployr-api-docs/#delete-workspace-object)以删除不必要的对象。 

   ```python
   #Create a snapshot of the current session.
   response = client.create_snapshot(session_id, deployrclient.models.CreateSnapshotRequest("Iris Snapshot"), headers)
   
   #Return the snapshot ID for reference when you publish later.
   response.snapshot_id
   
   #If you forget the ID, list every snapshot to get the ID again.
   for snapshot in client.list_snapshots(headers):
       print(snapshot)
   ```

### <a name="step-4-publish-the-model"></a>步骤 4. 发布模型 

已生成你的客户端库，并已将身份验证逻辑内置在你的应用程序后，你可以与核心 Api 创建 Python 会话、 创建模型时，和然后发布 web 服务使用该模型进行交互。

> [!NOTE]
> 请记住，你必须先进行身份验证您进行任何 API 调用。 因此，包括`headers`中的每个请求。

+ 将此 SVM 模型发布为机器学习服务器中的 Python web 服务。 此 web 服务将评分获取传递给它一个向量。

> [!IMPORTANT]
> 若要确保 web 服务注册为 Python 服务，请务必指定`runtime_type="Python"`。 如果不将运行时类型设为 Python，则默认为。

```python
   #Define a web service that determines the iris species by scoring 
   #a vector of sepal length and width, petal length and width
   
   #Set `flower_data` for the sepal and petal length and width
   flower_data = deployrclient.models.ParameterDefinition(name = "flower_data", type = "vector")
   #Set `iris_species` for the species of iris
   iris_species = deployrclient.models.ParameterDefinition(name = "iris_species", type = "vector")
   
   #Define the publish request for the web service and its arguments.
   #Specify the code, inputs, outputs, and snapshot.
   #Don't forget to set runtime_type="Python"`.
   publish_request = deployrclient.models.PublishWebServiceRequest(
       code = "iris_species = [names[x] for x in clf.predict(flower_data)]", 
       input_parameter_definitions = [flower_data], 
       output_parameter_definitions = [iris_species],
       runtime_type = "Python",
       snapshot_id = response.snapshot_id)

   #Publish the service using the specified name (iris), version (V1.0)
   client.publish_web_service_version("Iris", "V1.0", publish_request, headers)
```

### <a name="step-5-consume-the-web-service"></a>步骤 5. 使用 web 服务

本部分演示如何在被创建时所在的同一会话中使用的服务。

1. 在同一会话中，为服务中获取服务库存和元数据。

   ```python
   # Inspect holdings and metadata for service Iris V1.0.
   for service in client.get_web_service_version("Iris","V1.0", headers):
       #print service metadata (description, who published,...)
       print(service)
       #Print input and output parameters as defined in service definition object
       print("Input Parameters: {0}".format([str(parameter) for parameter in service.input_parameter_definitions]))
       print("Output Parameters: {0}".format([str(parameter) for parameter in service.output_parameter_definitions]))
   ```

2. 检查服务控股并准备使用。 
   ```python
   #Import the requests library to make requests on the server
   import requests
   #Import the JSON library to use for pretty printing of json responses
   import json

   #Create a requests `Session` object.
   s = requests.Session()

   #Record the R Server endpoint URL hosting the web services you created
   url = "http://localhost:12800"

   #Give the request.Session object the authentication headers 
   #so you don't have to repeat it with each request.
   s.headers = headers

   # Retrieve the service-specific swagger file using the requests library.
   swagger_resp = s.get(url+"/api/Iris/V1.0/swagger.json")

   #Either download service-specific swagger file using the json library.
   with open('iris_swagger.json','w') as f:
      (json.dump(client.get_web_service_swagger("Iris","V1.0",headers),f, indent = 1))

   #Or print just what you need from the Swagger file, 
   #such as the routing paths for the endpoints to be consumed.
   print(json.dumps(swagger_resp.json()["paths"], indent = 1, sort_keys = True))

   #Or, print input and output parameters as defined in the Swagger.io format
   print("Input")
   print(json.dumps(swagger_resp.json()["definitions"]["InputParameters"], indent = 1, sort_keys = True))
   print("Output")
   print(json.dumps(swagger_resp.json()["definitions"]["WebServiceResult"], indent = 1, sort_keys = True))
   ```

3. 通过提供一些使用该服务输入和获取 Iris 指定。 
   ```python
   #Make the request to consume the service using these flower_data inputs
   resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[7,3.2,4.7,1.4]})
   #Print the output
   print(json.dumps(resp.json(), indent = 1, sort_keys = True))

   ##Use input from another Iris species.
   resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[3,2.6,3,2.5]})
   print(json.dumps(resp.json(), indent = 1, sort_keys = True))

   ##Use input from another Iris species.
   resp = s.post(url+"/api/Iris/V1.0",json={"flower_data":[5.1,3.5,1.4,.2]})
   print(json.dumps(resp.json(), indent = 1, sort_keys = True))
   ```

## <a name="managing-the-services"></a>管理服务

现在，你已创建 web 服务，可以更新、 删除或重新发布该服务。 你还可以列出使用 Microsoft 机器学习服务器承载的所有 web 服务。

### <a name="update-a-web-service"></a>更新 web 服务

你可以更新 web 服务以更改的代码、 模型、 说明、 输入、 输出和的详细信息。 在此示例中，我们更新服务以将有用的说明添加到可能会使用此服务的人员。

```python
#Define what needs to be updated. Here we add a description.
#Be sure to specify the runtime_type again.
update_request = deployrclient.models.PublishWebServiceRequest(
    description = "Determines iris species using length and width of sepal and petal", runtime_type = "Python")
#Now update it by specifying the service name and version number
client.patch_web_service_version("Iris", "V1.0", update_request, headers)
```

### <a name="publish-another-version"></a>发布另一个版本

你还可以发布 web 服务的另一个的版本。 在此示例中，则服务会现在返回为字符串而不是一个字符串列表的 Iris 指定。

```python
#Publish another version of the web service, but this time 
#the service returns the species as a string instead of list of strings.
flower_data = deployrclient.models.ParameterDefinition(name = "flower_data", type = "vector")
iris_species = deployrclient.models.ParameterDefinition(name = "iris_species", type = "string")
 
#Define the publish request for the service and its arguments.
#Specify the changed code, inputs, outputs, and snapshot.
#Don't forget to set runtime_type="Python"`.
publish_request = deployrclient.models.PublishWebServiceRequest(
    code = "iris_species = [names[x] for x in clf.predict(flower_data)][0]",
    description = "Determines the species of iris, based on Sepal Length, Sepal Width, Petal Length and Petal Width",
    input_parameter_definitions = [flower_data],
    output_parameter_definitions = [iris_species],
    runtime_type = "Python",
    snapshot_id = response.snapshot_id)
 
#Now, publish the service with version (V2.0)
client.publish_web_service_version("Iris", "V2.0", publish_request, headers)
 
#Make request to consume service using these flower_data inputs; print output
resp = s.post(url+"/api/Iris/V2.0",json={"flower_data":[5.1,3.5,1.4,.2]})
print(json.dumps(resp.json(), indent = 1, sort_keys = True))
```

### <a name="list-services"></a>列出服务

获取所有 web 服务，包括那些由其他用户或在不同语言中创建的列表。

```python
#Return the list of all existing web services.
for service in client.get_all_web_services(headers):
    #print the service information
    print(service)
    #Print each input and output parameter
    print("Input Parameters: {0}".format([str(parameter) for parameter in service.input_parameter_definitions]))
    print("Output Parameters: {0}".format([str(parameter) for parameter in service.output_parameter_definitions]))
``` 

### <a name="delete-services"></a>删除服务

你可以删除已创建的服务。 如果你被分配到具有适当的权限的角色，你还可以删除其他服务。

在此示例中，我们会删除我们刚刚发布的第二个 web 服务版本。

```python
#Delete the second version we just published.
client.delete_web_service_version("Iris","V2.0",headers)
```

