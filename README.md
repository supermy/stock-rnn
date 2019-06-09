### Predict stock market prices using RNN

Check my blog post "Predict Stock Prices Using RNN": [Part 1](https://lilianweng.github.io/lil-log/2017/07/08/predict-stock-prices-using-RNN-part-1.html) and [Part 2](https://lilianweng.github.io/lil-log/2017/07/22/predict-stock-prices-using-RNN-part-2.html) for the tutorial associated.

One thing I would like to emphasize that because my motivation is more on demonstrating how to build and train an RNN model in Tensorflow and less on solve the stock prediction problem, I didn't try too hard on improving the prediction outcomes. You are more than welcome to take this repo as a reference point and add more stock prediction related ideas to improve it. Enjoy.

1. Make sure `tensorflow` has been installed.
2. First download the full S&P 500 data from [Yahoo! Finance ^GSPC](https://finance.yahoo.com/quote/%5EGSPC?p=^GSPC) (click the "Historical Data" tab and select the max time period). And save the .csv file to `data/SP500.csv`.
3. Run `python data_fetcher.py` to download the prices of individual stocks in S & P 500, each saved to `data/{{stock_abbreviation}}.csv`.
(NOTE: Google Finance API returns the prices for 4000 days maximum. If you are curious about the data in even early times, try modify `data_fetcher.py` code to send multiple queries for one stock. Here is the data archive ([stock-data-lilianweng.tar.gz](https://drive.google.com/open?id=1QKVkiwgCNJsdQMEsfoi6KpqoPgc4O6DD)) of stock prices I crawled up to Jul, 2017. Please untar this file to replace the "data" folder in the repo for test runs.)
4. Run `python main.py --help` to check the available command line args.
5. Run `python main.py` to train the model.


For examples,
- Train a model only on SP500.csv; no embedding
```bash
python main.py --stock_symbol=SP500 --train --input_size=1 --lstm_size=128 --max_epoch=50
```

- Train a model on 100 stocks; with embedding of size 8
```bash
python main.py --stock_count=100 --train --input_size=1 --lstm_size=128 --max_epoch=50 --embed_size=8
```

- Start your Tensorboard
```bash
cd stock-rnn
mkdir logs
tensorboard --logdir ./logs --port 1234 --debug
```

My python environment 当前的 Pyhon 环境: 
Python version == 2.7
```
BeautifulSoup==3.2.1 是一个可以从HTML或XML文件中提取数据的Python库
numpy==1.13.1 支持大量的维度数组与矩阵运算，此外也针对数组运算提供大量的数学函数库。
pandas==0.16.2 pandas 是基于NumPy 的一种工具，该工具是为了解决数据分析任务而创建的。Pandas 纳入了大量库和一些标准的数据模型，提供了高效地操作大型数据集所需的工具。pandas提供了大量能使我们快速便捷地处理数据的函数和方法。
scikit-learn==0.16.1 通用机器学习库,sklearn更倾向于使用者可以自行对数据进行处理，比如选择特征、压缩维度、转换格式，是传统机器学习库。
scipy==0.19.1 是构建在numpy的基础之上的,包括了统计、优化、整合以及线性代数模块、傅里叶变换、信号和图像图例，常微分方差的求解等。
tensorflow==1.2.1 一个基于数据流编程（dataflow programming）的符号数学系统，被广泛应用于各类机器学习（machine learning）算法的编程实现，其前身是谷歌的神经网络算法库DistBelief。
urllib3==1.8 Urllib3是一个功能强大，条理清晰，用于HTTP客户端的Python库。
```
