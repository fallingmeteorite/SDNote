---
title: ControlNet 应用
---
# ControlNet 应用
在 ControlNet 出现之前，控制图片的生成靠的是提示词，再加上图生图的局部重绘辅助。但在 ControlNet 出现后，控制图片变得简单了，通过图片 + 提示词的方式来更好的控制图片生成，还可以配合图生图进行生图。


## ControlNet 扩展
如果需要使用 ControlNet，需要安装 sd-webui-controlnet 扩展。

!!!note
    1. sd-webui-controlnet 扩展下载：https://github.com/Mikubill/sd-webui-controlnet。
	2. sd-webui-controlnet 扩展部分预处理器模型文件官方下载地址：https://huggingface.co/lllyasviel/Annotators/tree/main。
	3. sd-webui-controlnet 扩展模型文件官方下载地址：https://github.com/Mikubill/sd-webui-controlnet/wiki/Model-download。
	4. **预处理器模型文件** 用于 **预处理器** 项，**模型文件** 用于 **模型** 项。
	5. sd-webui-controlnet 扩展 **并不会** 主动下载预处理器模型文件 / 模型文件，默认情况下，您需要主动的去下载模型文件并放置到对应的文件夹。而预处理器文件在首次使用对应预处理器时从网络下载。

如果您打算主动下载预处理器模型文件，请将下载的文件按照以下折叠内容放置到对应的文件夹内。

???点击展开
    stable-diffusion-webui/extensions/sd-webui-controlnet/annotator/downloads <br/>
	├── [anime_face_segment/UNet.pth](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/anime_face_segment/UNet.pth) <br/>
	├── [clip_vision/clip_g.pth](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/clip_vision/clip_g.pth) <br/>
	├── [clip_vision/clip_h.pth](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/clip_vision/clip_h.pth) <br/>
	├── [clip_vision/clip_vitl.pth](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/clip_vision/clip_vitl.pth) <br/>
	├── [densepose/densepose_r50_fpn_dl.torchscript](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/densepose/densepose_r50_fpn_dl.torchscript) <br/>
	├── [depth_anything/depth_anything_vitl14.pth](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/depth_anything/depth_anything_vitl14.pth) <br/>
	├── [hand_refiner/hr16/ControlNet-HandRefiner-pruned/graphormer_hand_state_dict.bin](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/hand_refiner/hr16/ControlNet-HandRefiner-pruned/graphormer_hand_state_dict.bin) <br/>
	├── [hand_refiner/hr16/ControlNet-HandRefiner-pruned/hrnetv2_w64_imagenet_pretrained.pth](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/hand_refiner/hr16/ControlNet-HandRefiner-pruned/hrnetv2_w64_imagenet_pretrained.pth) <br/>
	├── [hed/ControlNetHED.pth](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/hed/ControlNetHED.pth) <br/>
	├── [insightface/models/antelopev2/1k3d68.onnx](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/insightface/models/antelopev2/1k3d68.onnx) <br/>
	├── [insightface/models/antelopev2/2d106det.onnx](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/insightface/models/antelopev2/2d106det.onnx) <br/>
	├── [insightface/models/antelopev2/genderage.onnx](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/insightface/models/antelopev2/genderage.onnx) <br/>
	├── [insightface/models/antelopev2/glintr100.onnx](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/insightface/models/antelopev2/glintr100.onnx) <br/>
	├── [insightface/models/antelopev2/scrfd_10g_bnkps.onnx](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/insightface/models/antelopev2/scrfd_10g_bnkps.onnx) <br/>
	├── [insightface/models/buffalo_l/1k3d68.onnx](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/insightface/models/buffalo_l/1k3d68.onnx) <br/>
	├── [insightface/models/buffalo_l/2d106det.onnx](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/insightface/models/buffalo_l/2d106det.onnx) <br/>
	├── [insightface/models/buffalo_l/det_10g.onnx](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/insightface/models/buffalo_l/det_10g.onnx) <br/>
	├── [insightface/models/buffalo_l/genderage.onnx](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/insightface/models/buffalo_l/genderage.onnx) <br/>
	├── [insightface/models/buffalo_l/w600k_r50.onnx](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/insightface/models/buffalo_l/w600k_r50.onnx) <br/>
	├── [lama/ControlNetLama.pth](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/lama/ControlNetLama.pth) <br/>
	├── [leres/latest_net_G.pth](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/leres/latest_net_G.pth) <br/>
	├── [leres/res101.pth](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/leres/res101.pth) <br/>
	├── [lineart/sk_model.pth](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/lineart/sk_model.pth) <br/>
	├── [lineart/sk_model2.pth](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/lineart/sk_model2.pth) <br/>
	├── [lineart_anime/netG.pth](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/lineart_anime/netG.pth) <br/>
	├── [manga_line/erika.pth](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/manga_line/erika.pth) <br/>
	├── [midas/dpt_hybrid-midas-501f0c75.pt](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/midas/dpt_hybrid-midas-501f0c75.pt) <br/>
	├── [mlsd/mlsd_large_512_fp32.pth](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/mlsd/mlsd_large_512_fp32.pth) <br/>
	├── [normal_bae/scannet.pt](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/normal_bae/scannet.pt) <br/>
	├── [normal_dsine/dsine.pt](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/normal_dsine/dsine.pt) <br/>
	├── [oneformer/150_16_swin_l_oneformer_coco_100ep.pth](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/oneformer/150_16_swin_l_oneformer_coco_100ep.pth) <br/>
	├── [oneformer/250_16_swin_l_oneformer_ade20k_160k.pth](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/oneformer/250_16_swin_l_oneformer_ade20k_160k.pth) <br/>
	├── [openpose/body_pose_model.pth](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/openpose/body_pose_model.pth) <br/>
	├── [openpose/dw-ll_ucoco_384.onnx](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/openpose/dw-ll_ucoco_384.onnx) <br/>
	├── [openpose/facenet.pth](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/openpose/facenet.pth) <br/>
	├── [openpose/hand_pose_model.pth](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/openpose/hand_pose_model.pth) <br/>
	├── [openpose/rtmpose-m_simcc-ap10k_pt-aic-coco_210e-256x256-7a041aa1_20230206.onnx](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/openpose/rtmpose-m_simcc-ap10k_pt-aic-coco_210e-256x256-7a041aa1_20230206.onnx) <br/>
	├── [openpose/yolox_l.onnx](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/openpose/yolox_l.onnx) <br/>
	├── [pidinet/table5_pidinet.pth](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/pidinet/table5_pidinet.pth) <br/>
	├── [TEED/7_model.pth](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/TEED/MTEED.pth) <br/>
	├── [uniformer/upernet_global_small.pth](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/uniformer/upernet_global_small.pth) <br/>
	└── [zoedepth/ZoeD_M12_N.pt](https://modelscope.cn/models/licyks/controlnet_v1.1_annotator/resolve/master/zoedepth/ZoeD_M12_N.pt)

安装后可在 SD WebUI 左下角的选项找到 ControNet 选项。

![controlnet_interface](../../assets/images/guide/controlnet
/controlnet_interface.jpg)

这里简单介绍 ControlNet 扩展的几个选项。

|功能|作用|
|---|---|
|图片导入框|上方导入图片的框就是导入作为控制条件的图片。|
|完美像素模式|可解决导入的控制图片和生成图片设置的宽高比例不同的问题。启用后 ControlNet 插件后，ControlNet 将会自动设置 Resolution 值（预处理器的分辨率），通常为最低可用分辨率。如果需要更高精度的预处理结果，需要禁用完美像素模式，手动调节  Resolution。|
|控制类型|调节不同的控制效果，一般选择后 ControlNet 扩展会自动选择相对应的预处理器和模型，部分情况下可能需要手动选择模型。|
|预处理器|处理导入的控制图片，使控制图片成为 ControlNet 模型可识别的控制条件。如果导入的控制图片已经经过预处理器处理过，则预处理器应选择无。预处理器有许多种，预处理图片的精度各不相同，可根据自己的需求进行选择。|
|模型|选择要使用的 ControlNet 模型。|
|中间的爆炸按钮（💥）|点击后可显示预处理器处理后的控制图片。|
|控制权重|调节 ControlNet 控制的强度。|
|引导介入 / 终止时机|调节 ControlNet 介入图片生成过程的时机。|
|控制模式|调节生图时提示词和 ControlNet 这两者所占的控制强度。|


## 不同 ControlNet 的作用
下面列出不同 ControlNet 的作用。

|种类|作用|控制图片|处理后的控制图片|效果图|
|---|---|---|---|---|
|[Canny](https://modelscope.cn/api/v1/models/licyks/controlnet_v1.1/repo?Revision=master&FilePath=control_v11p_sd15_canny_fp16.safetensors)|使用粗略的线条描绘图片中物体的边缘，生成线稿图。生图过程中使用线稿图约束物体的边缘。|![origin_canny](../../assets/images/guide/controlnet/origin_canny.jpg)|![preprocess_canny](../../assets/images/guide/controlnet/preprocess_canny.jpg)|![output_canny](../../assets/images/guide/controlnet/output_canny.jpg)|
|[Depth](https://modelscope.cn/api/v1/models/licyks/controlnet_v1.1/repo?Revision=master&FilePath=control_v11f1p_sd15_depth_fp16.safetensors)|生成一个灰度图，通过灰度的深浅描述物品的前后远近关系，指导大模型生成图片时物品的远近关系。|![origin_depth](../../assets/images/guide/controlnet/origin_depth.jpg)|![preprocess_depth](../../assets/images/guide/controlnet/preprocess_depth.jpg)|![output_depth](../../assets/images/guide/controlnet/output_depth.jpg)|
|[NormalMap](https://modelscope.cn/api/v1/models/licyks/controlnet_v1.1/repo?Revision=master&FilePath=control_v11p_sd15_normalbae_fp16.safetensors)|生成从输入图像派生的基本法线贴图，该图像使用了三种颜色：红色、绿色和蓝色。在 3D 程序领域，这些颜色用于确定物体表面的感知光滑度或凹凸度。每个颜色通道对应于一个特定的方向，例如左 / 右、上 / 下和近 / 远，从而可以在三维环境中模拟复杂的表面特征。|![origin_normalmap](../../assets/images/guide/controlnet/origin_normalmap.jpg)|![preprocess_normalmap](../../assets/images/guide/controlnet/preprocess_normalmap.jpg)|![output_normalmap](../../assets/images/guide/controlnet/output_normalmap.jpg)|
|[Openpose](https://modelscope.cn/api/v1/models/licyks/controlnet_v1.1/repo?Revision=master&FilePath=control_v11p_sd15_openpose_fp16.safetensors)|将图片中的人物动作分析出来，并生成骨骼图，指导大模型绘制人物时的动作。|![origin_openpose](../../assets/images/guide/controlnet/origin_openpose.jpg)|![preprocess_openpose](../../assets/images/guide/controlnet/preprocess_openpose.jpg)|![output_openpose](../../assets/images/guide/controlnet/output_openpose.jpg)|
|[MLSD](https://modelscope.cn/api/v1/models/licyks/controlnet_v1.1/repo?Revision=master&FilePath=control_v11p_sd15_mlsd_fp16.safetensors)|将图片中的场景（不包括人物）使用直线进行轮廓的大致描绘，生成大致的线条结构图。在生图过程通过线条结构图约束场景中大物件的边缘，常用于场景设计。|![origin_mlsd](../../assets/images/guide/controlnet/origin_mlsd.jpg)|![preprocess_mlsd](../../assets/images/guide/controlnet/preprocess_mlsd.jpg)|![output_mlsd](../../assets/images/guide/controlnet/output_mlsd.jpg)|
|[Lineart](https://modelscope.cn/api/v1/models/licyks/controlnet_v1.1/repo?Revision=master&FilePath=control_v11p_sd15s2_lineart_anime_fp16.safetensors)|使用更加精细的线条对图片进行描绘，生成线稿图。在生图过程中通过线稿图约束物体的边缘，常用于比较精细地还原物品的结构，保持构图结构。|![origin_lineart](../../assets/images/guide/controlnet/origin_lineart.jpg)|![preprocess_lineart](../../assets/images/guide/controlnet/preprocess_lineart.jpg)|![output_lineart](../../assets/images/guide/controlnet/output_lineart.jpg)|
|[Softedge](https://modelscope.cn/api/v1/models/licyks/controlnet_v1.1/repo?Revision=master&FilePath=control_v11p_sd15_softedge_fp16.safetensors)|将图片中物体的边缘用软边缘线条进行描绘，生成线条图。在生图过程中通过线条图约束物体的边缘，常用于还原物品的大致结构，保持构图结构。|![origin_softedge](../../assets/images/guide/controlnet/origin_softedge.jpg)|![preprocess_softedge](../../assets/images/guide/controlnet/preprocess_softedge.jpg)|![output_softedge](../../assets/images/guide/controlnet/output_softedge.jpg)|
|[Scribble](https://modelscope.cn/api/v1/models/licyks/controlnet_v1.1/repo?Revision=master&FilePath=control_v11p_sd15_scribble_fp16.safetensors)|将图片处理成涂鸦，类似手绘的效果，然后利用生成的涂鸦图片指导大模型生图，常用于自己画一张粗糙的涂鸦，使用该涂鸦来生成一张效果不错的图片。|![origin_scribble](../../assets/images/guide/controlnet/origin_scribble.jpg)|![preprocess_scribble](../../assets/images/guide/controlnet/preprocess_scribble.jpg)|![output_scribble](../../assets/images/guide/controlnet/output_scribble.jpg)|
|[Segmentation](https://modelscope.cn/api/v1/models/licyks/controlnet_v1.1/repo?Revision=master&FilePath=control_v11p_sd15_seg_fp16.safetensors)|将图片进行语义分割，将不同的画面元素用不同的颜色进行标注，生成语义分割图。在生图的过程中使用语义分割图指导大模型在对应的区域绘制不同颜色对应的物品，常用于大致规划图片构图。|![origin_segmentation](../../assets/images/guide/controlnet/origin_segmentation.jpg)|![preprocess_segmentation](../../assets/images/guide/controlnet/preprocess_segmentation.jpg)|![output_segmentation](../../assets/images/guide/controlnet/output_segmentation.jpg)|
|[Shuffle](https://modelscope.cn/api/v1/models/licyks/controlnet_v1.1/repo?Revision=master&FilePath=control_v11e_sd15_shuffle_fp16.safetensors)|将图片进行随机变换，然后将变换后的图像作为参考，指导图片生成的过程（风格迁移）。|![origin_shuffle](../../assets/images/guide/controlnet/origin_shuffle.jpg)|![preprocess_shuffle](../../assets/images/guide/controlnet/preprocess_shuffle.jpg)|![output_shuffle](../../assets/images/guide/controlnet/output_shuffle.jpg)|
|[Tile/Blur](https://modelscope.cn/api/v1/models/licyks/controlnet_v1.1/repo?Revision=master&FilePath=control_v11f1e_sd15_tile_fp16.safetensors)|Tile 将图片分割成一个个小区快，在对每个小区快进行重绘。Tile 不仅可以用作图片放大，增加图片的细节，也可以保持图片的整体构图不被改变，可用于风格转换。Blur 将图片进行高斯模糊，用作生成图片的参考，有点类似图生图，但整体构图不会改变太多。|![origin_tile](../../assets/images/guide/controlnet/origin_tile.jpg)|![preprocess_tile](../../assets/images/guide/controlnet/preprocess_tile.jpg)|![origin_tile](../../assets/images/guide/controlnet/origin_tile.jpg)|
|[Inpaint](https://modelscope.cn/api/v1/models/licyks/controlnet_v1.1/repo?Revision=master&FilePath=control_v11p_sd15_inpaint_fp16.safetensors)|重绘画笔涂抹过的区域，和 SD WebUI 自带的局部重绘功能类似。|![origin_inpaint](../../assets/images/guide/controlnet/origin_inpaint.jpg)|![preprocess_inpaint](../../assets/images/guide/controlnet/preprocess_inpaint.jpg)|![output_inpaint](../../assets/images/guide/controlnet/output_inpaint.jpg)|
|[InstructP2P](https://modelscope.cn/api/v1/models/licyks/controlnet_v1.1/repo?Revision=master&FilePath=control_v11e_sd15_ip2p_fp16.safetensors)|将提示词作为命令，指定修改图片中的元素，但不改变构图。|![origin_instructp2p](../../assets/images/guide/controlnet/origin_instructp2p.jpg)|![preprocess_instructp2p](../../assets/images/guide/controlnet/preprocess_instructp2p.jpg)|![output_instructp2p](../../assets/images/guide/controlnet/output_instructp2p.jpg)|
|Reference|将输入的图片作为参考，有点类似图生图。相对于图生图的效果，画面有着更多样的变化，不会过于呆板，输入图的风格也能迁移到生成出来的图片中。|![origin_reference](../../assets/images/guide/controlnet/origin_reference.jpg)|![preprocess_reference](../../assets/images/guide/controlnet/preprocess_reference.jpg)|![output_reference](../../assets/images/guide/controlnet/output_reference.jpg)|
|[Recolor](https://modelscope.cn/api/v1/models/licyks/controlnet_v1.1/repo?Revision=master&FilePath=ioclab_sd15_recolor.safetensors)|根据提示词的描述，对黑白的图片进行上色|![origin_recolor](../../assets/images/guide/controlnet/origin_recolor.jpg)|![preprocess_recolor](../../assets/images/guide/controlnet/preprocess_recolor.jpg)|![output_recolor](../../assets/images/guide/controlnet/output_recolor.jpg)|
|Revision|使用 CLIP Vision 分析图片，并指导图片的生成。|![origin_revision](../../assets/images/guide/controlnet/origin_revision.jpg)|![preprocess_revision](../../assets/images/guide/controlnet/preprocess_revision.jpg)|![output_revision](../../assets/images/guide/controlnet/output_revision.jpg)|
|[IP-Adapter](https://modelscope.cn/api/v1/models/licyks/controlnet_v1.1/repo?Revision=master&FilePath=ip-adapter_sd15_plus.pth)|使用 CLIP Vision 分析输入图片的信息，并将得出的信息作用于图像的生成过程中，常用于迁移画风，并搭配其他控制构图的 Controlnet 一起使用。|![origin_ipadapter](../../assets/images/guide/controlnet/origin_ipadapter.jpg)|![preprocess_ipadapter](../../assets/images/guide/controlnet/preprocess_ipadapter.jpg)|![output_ipadapter](../../assets/images/guide/controlnet/output_ipadapter.jpg)|

!!!note
    点击种类的名称可下载对应的 ControlNet 模型，ControlNet 模型放置在 stable-diffusion-webui/models/ControlNet 路径中

不同的 ControlNet 可组合起来一起使用，实现不同的效果。

***

## ControlNet 预处理器和 ControlNet 模型的关系
ControlNet 模型在控制图片的生成时，需要使用一张图作为参考，但是 ControlNet 模型并不认识普通的图片，所以这就需要使用 ControlNet 预处理将图片处理成 ControlNet 模型认识的图片。

ControlNet 预处理器后的图片如上方[不同 ControlNet 的作用](./controlnet.md#controlnet_2)部分中表格的处理后的控制图片的一样的效果。如果给 ControlNet 模型参考的图片是已经经过 ControlNet 处理过的图片时，就不需要再次经过 ControlNet 预处理器进行处理。

ControlNet 预处理器并不参与生图的采样过程，所以并不存在只兼容 Stable Diffusion 1.5 或者 Stable Diffusion XL 的说法。而 ControlNet 模型参与生图过程的采样过程，所以需要使用匹配版本的 Stable Diffusion 模型，如果出现`mat1 and mat2 shapes cannot be multiplied`这种报错，这就说明 ControlNet 模型和 Stable Diffusion 模型的版本不匹配。


## ControlNet 使用
下面介绍不同 ControlNet 控制类型的使用。

### ControlNet Scribble / Canny / MLSD / Softedge / Lineart
该控制类型属于边缘类控制，Scribble / Canny / MLSD / Softedge / Lineart 控制的精度各不同。

对画面的控制的精度：Scribble < Canny < Softedge < MLSD < Lineart


#### Scribble
这个 ControlNet 类型通常用于将涂鸦转换为图片，可以发挥自己的灵魂画技画一张草稿，再用 ControlNet Scribble 将涂鸦转换为一张想要的壁纸。

![use_scribble_controlnet_type](../../assets/images/guide/controlnet/use_scribble_controlnet_type.png)

ControlNet 扩展下方可以调节 Scribble 预处理器的效果。

|参数|作用|
|---|---|
|Resolution|调节预处理器的分辨率。|
|XDoG Threshold（scribble_xdog 预处理器）|设置边缘检测灵敏度。较低的值将导致检测到更多的边缘，从而可能捕获更精细的细节，而较高的值将集中在更突出的边缘上，从而减少杂色。|

下面是不同预处理器效果。

|预处理器|无|scribble_pidinet|scribble_xdog|scribble_hed|
|---|---|---|---|---|
|效果图|![image_before_preprocess_for_scribble](../../assets/images/guide/controlnet/image_before_preprocess_for_scribble.png)|![scribble_pidinet_preprocess](../../assets/images/guide/controlnet/scribble_pidinet_preprocess.png)|![scribble_xdog_preprocess](../../assets/images/guide/controlnet/scribble_xdog_preprocess.png)|![scribble_hed_preprocess](../../assets/images/guide/controlnet/scribble_hed_preprocess.png)|


#### Canny
Canny 控制类型的相比于 Scribble，精确度就比较高，可以用于复刻图片或者做艺术字等。

|![use_canny_controlnet_type_1](../../assets/images/guide/controlnet/use_canny_controlnet_type_1.png)|![use_canny_controlnet_type_2](../../assets/images/guide/controlnet/use_canny_controlnet_type_2.png)|
|---|---|

ControlNet 扩展下方可以调节 Canny 预处理器的效果。

|参数|作用|
|---|---|
|Resolution|调节预处理器的分辨率。|
|Low Threshold|去掉过细的线段。大于低阈值的线段被认定为边缘。|
|High Threshold|去掉零散的线段。大于高阈值的线段被认定为强边缘，全部保留；高阈值和低阈值之间的线段认定为弱边缘，只保留强边缘相邻的弱边缘。|


#### MLSD
MLSD 比较特殊，使用 MLSD 的预处理图片时，预处理器只会识别到图片中包含直线的部分（通常是建筑，物体），其他部分并不会识别到（如人物），所以这个控制类型适合控制建筑类的生成。

|![use_mlsd_controlnet_type_1](../../assets/images/guide/controlnet/use_mlsd_controlnet_type_1.png)|![use_mlsd_controlnet_type_2](../../assets/images/guide/controlnet/use_mlsd_controlnet_type_2.png)|
|---|---|

ControlNet 扩展下方可以调节 MLSD 预处理器的效果。

|参数|作用|
|---|---|
|Resolution|调节预处理器的分辨率。|
|MLSD Value Threshold|直线阈值。值越低，检测的直线越多。|
|MLSD Distance Threshold|距离阈值。对检测的之间进行距离筛选。|


#### Softedge
Softedge 的精度较高，预处理出的控制图片的边缘更加平滑，并且忽略内部的细节，可以让 AI 有更多的发挥空间。

![use_softedge_controlnet_type](../../assets/images/guide/controlnet/use_softedge_controlnet_type.png)

ControlNet 下方可以调节 Softedge 预处理器的效果。

|参数|作用|
|---|---|
|Resolution|调节预处理器的分辨率。|
|Safe Steps（softedge_teed、softedge_anyline 预处理器）|这个值越大，预处理得到的图片画面越干净。|

下面是不同预处理器效果。

|预处理器|无|softedge_pidinet|softedge_teed|softedge_pidisafe|softedge_hedsafe|softedge_hed|softedge_anyline|
|---|---|---|---|---|---|---|---|
|效果图|![image_before_preprocess_for_softedge](../../assets/images/guide/controlnet/image_before_preprocess_for_softedge.png)|![softedge_pidinet](../../assets/images/guide/controlnet/softedge_pidinet.png)|![softedge_teed](../../assets/images/guide/controlnet/softedge_teed.png)|![softedge_pidisafe](../../assets/images/guide/controlnet/softedge_pidisafe.png)|![softedge_hedsafe](../../assets/images/guide/controlnet/softedge_hedsafe.png)|![softedge_hed](../../assets/images/guide/controlnet/softedge_hed.png)|![softedge_anyline](../../assets/images/guide/controlnet/softedge_anyline.png)|


#### Lineart
Lineart 控制类型的精度最高，可以用于线稿上色等。

![use_lineart_controlnet_type](../../assets/images/guide/controlnet/use_lineart_controlnet_type.png)

!!!note
	如果控制图片是白底线稿，只需要 invert 预处理器将导入的图片进行反色就成为 ControlNet Lineart 的控制图片了。

ControlNet 下方可以调节 Lineart 预处理器的效果。

|参数|作用|
|---|---|
|Resolution|调节预处理器的分辨率。|

下面是不同 Lineart 预处理器的效果。

|预处理器|无|lineart_standard|lineart_realistic|lineart_coarse|lineart_anime_denoise|lineart_anime|
|---|---|---|---|---|---|---|
|效果图|![image_before_preprocess_for_lineart](../../assets/images/guide/controlnet/image_before_preprocess_for_lineart.png)|![lineart_standard](../../assets/images/guide/controlnet/lineart_standard.png)|![lineart_realistic](../../assets/images/guide/controlnet/lineart_realistic.png)|![lineart_coarse](../../assets/images/guide/controlnet/lineart_coarse.png)|![lineart_anime_denoise](../../assets/images/guide/controlnet/lineart_anime_denoise.png)|![lineart_anime](../../assets/images/guide/controlnet/lineart_anime.png)|


### ControlNet NormalMap / Depth / Segmentation
这类控制类型类似边缘控制，也能提供比较高的精度控制。

#### NormalMap
该控制类型通过法线贴图进行控制，可以为 AI 提供方位信息用于生成，可以更加精准的控制生成的图片中的元素方位，如人物面向的方向等。

![use_normal_map_controlnet_type](../../assets/images/guide/controlnet/use_normal_map_controlnet_type.png)

ControlNet 下方可以调节 NormalMap 预处理器的效果。

|参数|作用|
|---|---|
|Resolution|调节预处理器的分辨率。|
|Normal Background Threshold（normal_midas 预处理器）|控制图片中多远的背景元素被消除，该值越高，法线贴图中远处部分消失的越多。|
|Fov（normal_dsine 预处理器）|控制在任何给定时刻看到的可观察世界的范围，影响输入图像的透视来影响法线贴图的生成方式。较高的值会使视图更宽，捕获更多的场景，而较低的值会缩小视图。|
|Iterations（normal_dsine 预处理器）|设置预处理器的迭代步数，类似图片生成参数中的迭代步数。值越高，预处理得到的发现贴图质量越高。|

下面是不同预处理器的效果。

|预处理器|无|normal_bae|normal_midas|normal_dsine|
|---|---|---|---|---|
|效果图|![image_before_preprocess_for_normal_map](../../assets/images/guide/controlnet/image_before_preprocess_for_normal_map.png)|![normal_bae](../../assets/images/guide/controlnet/normal_bae.png)|![normal_midas](../../assets/images/guide/controlnet/normal_midas.png)|![normal_dsine](../../assets/images/guide/controlnet/normal_dsine.png)|


#### Depth
该控制类型通过灰度图中带的远近前后关系，控制 AI 生成元素时的远近前后关系。

![use_depth_controlnet_type](../../assets/images/guide/controlnet/use_depth_controlnet_type.png)

ControlNet 下方可以调节 Depth 预处理器的效果。

|参数|作用|
|---|---|
|Resolution|调节预处理器的分辨率。|
|Remove Near %（depth_leres++ / depth_leres 预处理器）|将较亮的区域剪辑为全白，从而有效地将图像的较近部分涂抹为平面，就像卡通人物撞到一块玻璃一样。值越高，深度贴图的近处部分就越容易被压平和模糊。|
|Remove Background %（depth_leres++ / depth_leres 预处理器）|将较暗的区域剪辑为全黑，从而有效地使它们消失在阴影中。值越高，深度贴图的远处部分消失得越多。这对于剪切背景中不需要的元素非常有用。|

下面是不同预处理器的效果。

|预处理器|无|depth_midas|depth_zoe|depth_leres++|depth_leres|depth_hand_refiner|depth_anything_v2|depth_anything|
|---|---|---|---|---|---|---|---|---|
|效果图|![image_before_preprocess_for_depth](../../assets/images/guide/controlnet/image_before_preprocess_for_depth.png)|![depth_midas](../../assets/images/guide/controlnet/depth_midas.png)|![depth_zoe](../../assets/images/guide/controlnet/depth_zoe.png)|![depth_leres++](../../assets/images/guide/controlnet/depth_leres++.png)|![depth_leres](../../assets/images/guide/controlnet/depth_leres.png)|![depth_hand_refiner](../../assets/images/guide/controlnet/depth_hand_refiner.png)|![depth_anything_v2](../../assets/images/guide/controlnet/depth_anything_v2.png)|![depth_anything](../../assets/images/guide/controlnet/depth_anything.png)|

!!!note
	depth_hand_refiner 预处理器专门用于识别手部并只生成手部的深度图，因为该预处理器在训练时可能缺少二次元图片的训练集，所以对于二次元图片的手部识别较差。


#### Segmentation
该控制类型通过对图片进行语义分割，使用不同的颜色对图片元素进行标记，使模型在生成图片时能够根据颜色信息在对应的颜色位置生成对应的元素。

![use_segmentation_controlnet_type](../../assets/images/guide/controlnet/use_segmentation_controlnet_type.png)

!!!note
	Segmentation 分割图像使用的颜色对应的元素可参考：[大江户战士整理的Seg分隔.pdf](https://modelscope.cn/models/licyks/sdnote/resolve/master/other/%E5%A4%A7%E6%B1%9F%E6%88%B7%E6%88%98%E5%A3%AB%E6%95%B4%E7%90%86%E7%9A%84Seg%E5%88%86%E9%9A%94.pdf)。

ControlNet 下方可以调节 Segmentation 预处理器的效果。

|参数|作用|
|---|---|
|Resolution|调节预处理器的分辨率。|

下面是不同预处理器的效果。

|预处理器|无|seg_ofade20k|seg_ufade20k|seg_ofcoco|seg_anime_face|mobile_sam|
|---|---|---|---|---|---|---|
|效果图|![image_before_preprocess_for_segmentation](../../assets/images/guide/controlnet/image_before_preprocess_for_segmentation.png)|![seg_ofade20k](../../assets/images/guide/controlnet/seg_ofade20k.png)|![seg_ufade20k](../../assets/images/guide/controlnet/seg_ufade20k.png)|![seg_ofcoco](../../assets/images/guide/controlnet/seg_ofcoco.png)|![seg_anime_face](../../assets/images/guide/controlnet/seg_anime_face.png)|![mobile_sam](../../assets/images/guide/controlnet/mobile_sam.png)|



### ControlNet OpenPose
该控制类型通过骨架图，精准地控制人物动作。

![use_openpose_controlnet_type](../../assets/images/guide/controlnet/use_openpose_controlnet_type.png)

ControlNet 下方可以调节 OpenPose 预处理器的效果。

|参数|作用|
|---|---|
|Resolution|调节预处理器的分辨率。|

下面是不同预处理器的效果。

|预处理器|无|openpose_full|openpose_hand|openpose_faceonly|openpose_face|openpose|dw_openpose_full|densepose_parula|densepose|animal_openpose|
|---|---|---|---|---|---|---|---|---|---|---|
|效果图|![image_before_preprocess_for_openpose](../../assets/images/guide/controlnet/image_before_preprocess_for_openpose.png)|![openpose_full](../../assets/images/guide/controlnet/openpose_full.png)|![openpose_hand](../../assets/images/guide/controlnet/openpose_hand.png)|![openpose_faceonly](../../assets/images/guide/controlnet/openpose_faceonly.png)|![openpose_face](../../assets/images/guide/controlnet/openpose_face.png)|![openpose](../../assets/images/guide/controlnet/openpose.png)|![dw_openpose_full](../../assets/images/guide/controlnet/dw_openpose_full.png)|![densepose_parula](../../assets/images/guide/controlnet/densepose_parula.png)|![densepose](../../assets/images/guide/controlnet/densepose.png)|![animal_openpose](../../assets/images/guide/controlnet/animal_openpose.png)|

!!!note
	1. 因为部分预处理器在训练时训练集缺少二次元类型的图片，所以预处理器的识别效果较差。  
	2. 可以使用 [sd-webui-openpose-editor](https://github.com/huchenlei/sd-webui-openpose-editor) 扩展对骨架图进行编辑，导入图片到 ControlNet 扩展后，选择识别效果比较好的预处理器，如 dw_openpose_full，再点击 💥 对图片进行预处理，处理图片完成后可以在预处理结果看到处理好的图片，此时点击第二个**编辑**按钮进入 sd-webui-openpose-editor。  
    ![use_openpose_editor_to_edit_pose](../../assets/images/guide/controlnet/use_openpose_editor_to_edit_pose.png)  
    在里面对骨架图编辑好后，**点击发送姿势到ControlNet**，将编辑后的骨架图发送回 ControlNet 扩展中，再进行图片生成，这样可以得到比较好的效果。  
	3. sd-webui-openpose-editor 扩展下载：https://github.com/huchenlei/sd-webui-openpose-editor



<!-- TODO: 补充 ControlNet 的实际应用-->
<!-- TODO: 蒙版的作用 https://github.com/Mikubill/sd-webui-controlnet/discussions/2793 -->
<!-- TODO: 补充模型链接和选择 -->