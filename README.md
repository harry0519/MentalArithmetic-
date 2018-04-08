# MentalArithmetic 小学口算训练统计工具

平时纸质口算使用答题卷, 存在以下问题
* 题目固定.反复练习后, 小孩直接背诵答案顺序, 并未真正训练口算
* 题目数量有限, 没有全覆盖所有可能的题型
* 无法统计单题使用时间, 对答题情况进行精确分析
* 无法根据小孩答题情况, 动态调整出题频率

针对纸质试卷问题, MentalArithmetic工具提供
* 随机出题, 单次测试题目不重复
* 单题用时记录
* 答题完毕后的统计分析
* 长期记录分析(未实现)
* 根据历史答题时间, 动态调整出题频率. 针对性训练不熟练的题(未实现)
* 能力分析. 根据测试题记录, 给出口算速度提高的分析报告, 便于平时进行针对性训练.(未实现)

出题方式
* 随机出题
20以内加减法共20*2*20=800题. 考虑到一些不太需要练习的情况, MentalArithmetic去除了
	* 相减<=0 (a<=b)
	* 相加>20的题目 (a+b>20)
	* 含10和1的题
剩余题库=380题. 如果希望保留, 可以使用 -e参数: python emath.py -e

* 动态出题
当完成的随机出题数量超过300题后(答题8次后), 会自动触发动态出题(可以开始时输入's'保存随机出题模式).
动态出题时会统计最近300题用时,然后在用时最长的100题中随机抽取.如果同一题出现多次,使用算术平均作为答题时间.

# 环境
操作系统: 支持windows, macOS

环境搭建
* 安装python3.5+, https://www.python.org/downloads/
* 安装pip: https://pypi.python.org/pypi/pip#downloads , 
	* python setup.py install
* 安装第三方依赖库: pip install -r requirements.txt

环境配置对于非程序员可能比较困难,如果碰到问题可以在issue留言. 我也尝试了直接出exe包,但是考虑多系统的复杂性,没有计划做二进制发布.等功能晚上后,考虑会移植到微信小程序.


# 运行
默认单次试题数量未60题， 可以通过修改ematch.py文件中QUESTION_NUM 来调整单次试题数量. 建议在20-200题之间.
python emath.py

按enter后开始答题.
答出后马上按enter进入
答题完毕会显示本次答题的时间变化信息及整体, 加法,减法的统计分类信息.

# 分析
答题完成后, 所有历史答题记录会保存在anwser.csv文件中, 统计信息保存在history.csv文件中.

答题完成后统计图表
![答题统计图](https://github.com/harry0519/MentalArithmetic/blob/master/Figure_1.png)
* 左侧图表为本次答题所有题目详细时间.蓝色线段为本次答题单题时长变化线. 蓝线为本次答题平均时间, 红线为2秒(1分钟30题), 绿线为1秒(1分钟60题).
* 右侧上部蓝色为整体速度分布.x坐标:时间, y坐标:题目落在区间内的题目数量.
* 右侧中部/下部绿色柱状图分别为加法和减法的histgram 图
* 下方图表中, 蓝色线段为本次答题单题时长变化线. 红色参考线为2秒(1分钟30题), 绿色参考线为1秒(1分钟60题). 

# 其他
欢迎发送你小孩的成绩文件(emathis.csv),年龄, 性别, 城市给我:harry0519@gmail.com, 用于进一步的统计分析.
