# Superset 与 Kylin 集成

Superset 官方支持清单里没有 Kylin。但是由于 Superset 是通过 SQLAlchemy 访问数据源的，所以原则上只要实现一套 Kylin 的 SQLAlchemy 方言（dialect）+ DBAPI 实现，即可以对其做集成。



## 前提

已部署 Superset

已部署 Kylin



## 安装 PyKylin

Python 的官方库中没有找到 Kylin 的 SQLAlchemy + DBAPI 实现，但是在 GitHub 上有一个 [pykylin](https://github.com/wxiang7/pykylin) 项目。

由于 Kylin 在设计上与 Superset 有一些冲突，使用这个 pykylin 会有一些兼容性的问题。我在这个版本的基础上做了一些调整，使其可以兼容 Supset：

**pykylin4superset**：[https://github.com/YorkeCao/pykylin4superset](https://github.com/YorkeCao/pykylin4superset)

[点此下载]([https://codeload.github.com/YorkeCao/pykylin4superset/zip/master](https://codeload.github.com/YorkeCao/pykylin4superset/zip/master))其压缩文件，解压后进入其根目录，执行：

```
pip install -r ./requirements.txt
python setup.py install
```

**注意**！如果 Superset 安装在 virtualenv 虚拟机中，注意要在其虚拟环境中执行上述命令。

安装完成后，重新启动 Superset。



## 配置 Superset

现在可以配置 Kylin 数据源了。

进入添加 Database 的页面。

1. 在 Database 条目中任意起一个名字，如：ylinDB
2. 在 SQLAlchemy URI 中输入连接串，如：kylin://admin:KYLIN@localhost:7070/kylin/api?project=yourProjectName
3. 单击 **Test Connection** 测试链接
4. 测试成功后，点击 **Save** 保存

![](https://raw.githubusercontent.com/YorkeCao/pykylin4superset/master/assets/image/kylin00.png)

这样 Kylin 的数据源就创建好了。



## 测试

可以创建 Table，然后创建 Slice 进行测试。

