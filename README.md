# 算法文档汇总

kua.ai的算法roadmap、现有能力介绍、api文档都放在这个repo，供参考。


## CV 算法

### text 2 image

text to image，在团队内部被称为aigc，能根据用户输入的prompt，生成符合prompt语义的图片。

这个能力是由三个模型按先后顺序执行组合而成，分别是：

1.  将用户的prompt，转换成语义空间的向量，这个向量通常称为embedding。这个功能，用的是OpenAi的clip模型（https://github.com/openai/CLIP ）。
2.  第二个模型是diffusion架构模型，我们目前采用的是runwayML这家公司开源的diffusion模型。关于这个模型，有很多的名称：
    
    1. diffusion是一个算法设计的概念，中文叫扩散模型。
    2. 2022年的这些刷屏aigc能力，OpenAI的Dall E2, 谷歌的Imagen，Meta的作图，都使用了扩散模型；也就是说，大家用的模型如果画成示意图，应该都大同小异，只是
    大厂做得更好更大。
    3. stability AI、runwayML、慕尼黑大学的CV实验室，这三家一起合作，将他们的扩散模型开源了，他们开源的这一系列模型叫做stable diffusion，从v1一直到v4。
    4. 后面runwayML自己也开源了自己独立训练出来的扩散模型，他们已经不用stable diffusion这个名称了，只是说自己开源了这样的模型，可能是商标问题；
    5. 还有一些开源项目，例如Dall Mini，也将自己的扩散模型开源了，只是因为效果没有stable diffusion的好，所以没有太多商用。

    这个扩散模型，可以有两种使用方式：

    a. 将上面一步的语义embedding，一步到位，生成最终的图像，这个是谷歌的Imagen的做法，后续就不会再有其他模型了；
    
    b. 将上一步的语义embedding，使用扩散模型，再生成一个image embedding。

3. 第三个模型，是VAE模型，其作用是利用上面的image embedding，生成最终的图像。这个VAE模型，我们采用的是stable diffusion系列中的VAE模型。

4. 最后一个模型，是额外的safety checker，查验模型生成的图片是否黄暴，如果是，就返回一张全黑图片。这个safety checker，来自huggingface。

### inpainting

inpainting和上面的text2image，用的是一模一样的模型，执行流程也相类似，唯一的区别在2.a：
 
    - aigc中，语义embedding，是模型的唯一输入；
    - 在inpainting中，除了语义embedding，还有我们的initial_image, mask_image，作为扩散模型的输入；


因为aigc和inpainting的执行方式几乎一致，所以我们的api接口能做到只运行一个模型，就能提供两种服务。
### image segmentation

image segmentation对应的就是抠图功能。

目前开源的image segmentation，尤其是通用的物品抠图，DIS(https://github.com/xuebinqin/DIS)是业界最实用的。

### image composition

对应的功能是图片合成。





