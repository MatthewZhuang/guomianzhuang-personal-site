背景：传统i2i召回没有建模U2I部分(级联系统的限制)，无法直接对业务目标进行建模，会有全链路目标不一致的问题.

deepranki2i相比i2i前进一步，通过<trigger, item\>的线上表现，重新计算<trigger, item\>之间的similar score，但是需要注意的是仍旧没有解决U2I的建模问题.

ranki2i的做法有很多，简单做可以直接用场景效率分item相似分加权得到排序分,但是加权系数不好决策.

deepranki2i就是用模型的方式去学习排序规则，得到和业务目标一致的排序分.

deepranki2i学习的是<trigger, item\>对的序关系，有很多种方式去定义和构造损失函数.


- 基于triplet loss的序关系学习
    - step1: 基于线上反馈构造pair序关系，比如定义score(item|trigger) = w1\*cvr(item|trigger) + w2\*ctr(item|trigger),那么pair之间有了一个权重
    - step2: 样本1<trigger, item1, score\>, 给trigger随机采样一个item2,score2
    - step3: triplet_loss(t, i1, i2) = max(sign(score1-score2)\*(f(t,i2)-f(t,i1))+m, 0)
    - step4: 本质是希望函数f()可以学习到真实的score，所以可以限制mse(f, score),多任务学习.
- 也可以转为ctr任务来实现，<trigger, item\> -\> <user, item\>.
- 其他LTR的实现: TODO.

triplet loss人脸识别中常用的损失函数，针对pair 排序问题比较适用.


ranki2i：基于曝光样本对进行点击预估，转化效率更高，缺点也是仅能基于i2i召回曝光样本构建pair，无法打破闭环。
swingi2i优势：没有ranki2i的缺点，可以建立更多的item链接，但是效率不如ranki2i.








