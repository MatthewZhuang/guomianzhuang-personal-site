
paper: Exploring the Upper Limits of Text-Based Collaborative Filtering Using Large Language Models: Discoveries and Insights </br>

blog: [探索大语言模型LLM用于文本推荐的性能极限](https://zhuanlan.zhihu.com/p/646196122)

- TCF性能和参数量级的关系？
    - 参数量越大，TCF效率越高，千亿级别仍不是上限
- 基于LLM的TCF是否可以超越IDCF？
    - 采用transformer架构的CTR模型上，基于LLM表征的TCF可以和IDCF打平；在warm推荐的场景甚至可以超越；
- LLM是否可以提供通用物品表征？
    - 不能，对LLM产出的item embedding微调的效果要远远优于表征冻结的方式.所以特定场景数据对于embedding微调效率提升还是显著的.
- 基于LLM的TCF是否可以实现通用推荐大模型？
    - 实现通用推荐大模型的两个主要难点：1、去除ID，因为不同系统ID不通，所以要去掉，采用文本表征；2、效果迁移（不需要微调）；
    - 结论是目前还不能，效果远远达不到；
    - 文中指出，这是因为推荐系统不同于NLP和CV，推荐系统需要一个是item embedding具有通用性（上面的问题），第二个是<user, item>应该具有可迁移性，但是匹配策略和推荐系统的曝光策略有关。
    - 关于第二点，个人认为是非常具有挑战的，也是现在传统推荐系统一直在解决的马太效应和信息茧房问题。这里面涉及到三个问题，1、无偏数据集问题，2、模型训练，3、模型评估问题
    - 真正的通用推荐系统的提升将会是像现在LLM对NLP和CV领域的作用一样，将会在搜推广三大核心互联网场景产生地震一样的作用；



