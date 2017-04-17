>[!IMPORTANT]
>手动故障转移资源之后，需要删除在移动过程中自动添加的位置约束。

### <a name="remove-the-location-constraint"></a>删除位置约束

在手动移动过程中，`move` 命令会为要放置在新目标节点上的资源添加位置约束。 若要查看新约束，请在手动移动资源后运行以下命令：

```bash
sudo pcs constraint --full
```

需要删除位置约束，以便将来移动（包括自动故障转移）成功。 

若要删除约束，请运行以下命令。 在以下命令中，`ag_cluster-master` 是已移动的资源的名称。 请将此名称替换为你的资源名称：

```bash
sudo pcs resource clear ag_cluster-master 
```

或者，可以运行以下命令删除位置约束。 在以下命令中，`cli-prefer-ag_cluster-master` 是需要删除的约束的 ID。 `sudo pcs constraint --full` 会返回此 ID。  

```bash
sudo pcs constraint remove cli-prefer-ag_cluster-master  
```

>[!NOTE]
>自动故障转移不会添加位置约束，因此不需要进行清除。 

详细信息：
- [Red Hat - 管理群集资源](http://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/ch-manageresource-HAAR.html)
- [Pacemaker - 手动移动资源](http://clusterlabs.org/doc/en-US/Pacemaker/1.1-pcs/html/Clusters_from_Scratch/_move_resources_manually.html)
