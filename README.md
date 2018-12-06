### stage1 爬取数据

从[名字大全网站](http://www.resgain.net/xmdq.html)抓取了**1181270**个名字
从[顶点小说网《大医凌然》](https://www.booktxt.net/8_8985/)中抓取文本，通过jieba分词，获取了**32684**个非人名单词

上面获取的所有单词的长度都在**2~4**之间

### stage2 数据预处理

+ 将上述获取的数据都用'|'填充至长度为4
+ 然后对填充后的数据进行one-hot处理，字符与向量的对应关系的字典保存在__task3/obj/model2_c2i.pkl__文件中

### stage3 模型训练

+ 采用的模型是卷积神经网络是一个**8层**的卷积神经网络，其中三层进行了dropout处理，dropout值为0.1
+ 训练的正样本从1181279个人名中随机选取了50000个，加上32684个非人名单词总共为82684个训练样本
+ 随机选取其中的70000个样本作为训练样本，剩下的12684个样本作为测试样本
+ 训练模型的代码在train_model.ipynb内

### stage4 模型结果

+ 模型在训练集上的auc和准确率分别为：__0.9986408313637744__, __0.9987142857142857__
+ 模型在测试集上的auc和准确率分别为：__0.9735193137436282__, __0.9758751182592242__

### 模型的使用

+ 输入的字符必须是中文字符，目前模型支持的中文字符只有训练样本内的不到5000种字符，输入的字符不在其中会报错
+ 输入字符串的长度不能超过4，否则会报错
