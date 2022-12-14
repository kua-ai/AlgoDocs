## relight API

已有样品：

- https://clipdrop.co/blog/relight-technicalities 
    
    demo试玩

    关键在于 depth maps and surface normals.
    
    depth map用https://github.com/isl-org/MiDaS

    surface用来做texture的rendering

- https://github.com/EPFL-VILAB/omnidata#readme

    这一个似乎是能做depth和surface一起做的repo。

    https://github.com/EPFL-VILAB/omnidata/tree/main/omnidata_tools/torch#pretrained-models

    输出的是normal 和 depth，照理说，这两个就足够用于shadow生成了？

- https://huggingface.co/spaces/radames/dpt-depth-estimation-3d-voxels

    这个解决方案应该更对应光影的需求；

    这个解决方案能提供3d gltF格式的输出，这个是相当于jpeg的3d文件格式，非常适合webgl使用。


此处需要补充一点3D渲染的基础知识了：

- https://en.wikipedia.org/wiki/Heightmap

height map能转换为3D Mesh

- https://en.wikipedia.org/wiki/Normal_mapping

normal map就是贴皮肤。It is used to add details without using more polygons.

a normal map from a high polygon model or height map.似乎来自于网格模型，或者深度图，所以，深度图和normal map是不是一回事儿？




3d文件gltf的viewer;
https://gltf-viewer.donmccurdy.com/


### 测试结果


### 调用方式

### 参数

### 返回结果