
大洋云转码Python SDK
==================

安装
----
```
git clone git@git.hoge.cn:jeffkit/dytranscoder-py.git
cd dytranscoder
sudo python setup.py install
```

使用
----

```
>>> from dytranscoder import Dytranscoder
>>> dc = Dytranscoder('http://100.10.10.10')
>>> rsp = dc.addTranscodeTask(UserID='jeff', TaskID='xxxx',
                              SourceFile=dict(FileType=1, FileName='fi.png'),
                              TargetFile=dict(xxxxx))
>>> rsp.status
0
>>> rsp.description
success
>>> rsp.data
{}
```

每次API的调用都会有固定的返回格式,是一个APIResponse对象，该对象有三个属性：
- status, 状态码，0为成功，其异均为有错。
- description，对当前请求的响应描述，成功或失败的原因。
- data，响应数据。通常是一个字典。


方法调用规则
----------
每个API对应着Dytranscoder的一个方法，方法名就是接口路径的最后一段，如：
创建任务接口 /LeoVideoAPI/service/addTranscodeTask，对应的API方法就是：
dc.addTranscodeTask

方法接受的参数与文档中要求的参数同步，大小写请保持一致。
另外注意两种特殊情况：

- 同一个层级有两个或以上的同名标签，则该参数值使用list来表示。如查询任务状态，
可以使用多个TaskID，则调用方式应该这样：

```
>>> dc.queryTaskProgress(TaskID=['id2', 'id2'])
```

- 参数的值为复杂数据结构时，使用dict来组装。如创建任务的SourceFile、
TargetFile等都属于复杂数据结构。在构造它们的值时，请使用dict()。如上面完整的示例。
