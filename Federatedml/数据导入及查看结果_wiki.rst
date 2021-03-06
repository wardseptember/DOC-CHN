1. | **如何上传数据表？**
   | 具体上传流程参考这里的upload guide:
     https://github.com/FederatedAI/FATE/tree/master/doc
     数据上传到eggroll(存储及计算引擎)里面，在内部party里进行数据分发，变成后续算法可执行的DTable格式

2. | **如何删除已经上传的数据表**
     DTable提供destroy接口，table.destroy()就行了。具体流程如下：
     新建py脚本，执行以下代码: >from arch.api import session
   | #if version of FATE before v1.1, it should be
   | # from arch.api import eggroll
   | # and then eggroll instead of session
   | table_name = “your_table_name”
   | namespace = “your_namespace”
   | # mode = 0 for standalone and 1 for cluster
   | session.init(job_id=“a_test_jobid”, mode=1)
   | \_table = session.table(name=table_name, namespace=namespace)
   | print(“table count:{}”.format(_table.count()))
   | \_table.destroy()
   | print(“after destroy, table count:{}”.format(_table.count()))

3. | **如何使用某个算法，跑自己的数据？**
   | 首先，使用fate_flow上传自己的数据，记录下对应的table和table
     name，具体上传流程参考这里的upload guide:
     https://github.com/FederatedAI/FATE/tree/master/doc
     然后在example下有对应算法的文件夹，里面有例子的dsl和conf，把conf里面的数据table和table_name换成刚刚上传了的数据表。然后利用fate_flow的接口启动任务即可，具体启动命令，在文件夹下有README.
     dsl和对应conf的配置，根据需要自行修改

4. **如何查看组件数据输出**

   1. Fateboard可展示前100条
   2. https://github.com/FederatedAI/FATE/blob/master/fate_flow/doc/fate_flow_cli.md
      通过”component_output_data”指令查询

5. | **如何查看训练好的模型**
   | 主要有两种方式:

   1. Fateboard
   2. https://github.com/FederatedAI/FATE/blob/master/fate_flow/doc/fate_flow_cli.md
      通过”component_output_model”指令查询

6. | **各方数据需要准备什么？需要知道对方的features吗？**
   | 答：各方数据需要做一定的ETL加工处理，处理成可以建模的数据，比如是数值特征。联邦学习一方不需要知道另外一方的feature。

7. | **预处理有什么要求？**
   | 如果数据预处理，可以在数据导入前做好，处理成能建模的数据就可以，也可以用FATE系统自带一些特征工程处理工具。
