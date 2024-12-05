---
title: 杂项
---
# 杂项
这里列出其他在 SD WebUI 里用的功能。


## SD WebUI 不同路径 / 文件的作用
这是 SD WebUI 中不同路径 / 文件的作用。

|路径 / 文件|作用|
|---|---|
|stable-diffusion-webui/models|大部分模型的保存路径|
|stable-diffusion-webui/extensions|扩展路径|
|stable-diffusion-webui/extensions-builtin|SD WebUI 内置扩展路径|
|stable-diffusion-webui/outputs|生成图片的保存路径|
|stable-diffusion-webui/repositories|SD WebUI 内部组件|
|stable-diffusion-webui/cache.json|模型哈希记录文件|
|stable-diffusion-webui/config.json|保存 SD WebUI 设置的文件|
|stable-diffusion-webui/params.txt|保存上一次生图的参数|
|stable-diffusion-webui/styles.csv|提示词预设文件|
|stable-diffusion-webui/ui-config.json|SD WebUI 界面预设文件|

SD WebUI 在使用的时候会把部分模型放置在缓存路径中，路径如下。

|不同启动方式的用户|缓存路径|
|---|---|
|绘世启动器用户|stable-diffusion-webui/.cache|
|使用原生 SD WebUI 启动方式用户|C:/Users/%USERNAME%/.cache|

.cache 为隐藏路径，需要将文件管理器显示隐藏文件的功能打开，参看：[杂项 - 显示隐藏的文件和文件后缀名 - SDNote](../../help/other.md#_4)


## SD WebUI 中不同模型的放置路径
|模型种类|放置路径|
|---|---|
|Stable Diffusion 模型（大模型）|stable-diffusion-webui/models/Stable-diffusion|
|VAE 模型|stable-diffusion-webui/models/VAE|
|VAE-approx 模型|stable-diffusion-webui/models/VAE-approx|
|LoRA 模型|stable-diffusion-webui/models/Lora|
|Lycoris 模型<sup>1</sup>|stable-diffusion-webui/models/Lora </p> stable-diffusion-webui/models/LyCORIS|
|Embedding 模型|stable-diffusion-webui/embeddings|
|Hypernetwork 模型|stable-diffusion-webui/models/hypernetworks|
|高清修复模型|stable-diffusion-webui/models/ESRGAN </p> stable-diffusion-webui/models/RealESRGAN </p> stable-diffusion-webui/models/SwinIR </p> stable-diffusion-webui/models/DAT|
|ControlNet 模型<sup>2</sup>|stable-diffusion-webui/models/ControlNet </p> stable-diffusion-webui/extensions/sd-webui-controlnet/models|
|ControlNet 预处理器模型<sup>3</sup>|stable-diffusion-webui/extensions/sd-webui-controlnet/annotator/downloads|
|AnimateDiff 模型|stable-diffusion-webui/extensions/sd-webui-animatediff/model|
|TIPO 模型|stable-diffusion-webui/extensions/z-tipo-extension/models|

!!!note
    1. SD WebUI 1.5 及以上版本无需扩展即可读取 LyCORIS 文件夹内的 LyCORIS 模型（该文件夹不会自动生成），并显示在 SD WebUI 的 LoRA 栏内。
	2. 两个文件夹皆可放置 ControlNet 模型。
	3. 并非所有的 ControlNet 预处理器模型都存储在 downloads 文件夹（例如： depth_anything 预处理器的部分模型会存储在 .cache 文件夹内）。


## 图片信息查看
如果想要查看一张由 SD WebUI 生成的图片的参数，可以在 SD WebUI 的 PNG 图片信息里，导入图片后即可查看生图参数。

![png_info_view](../../assets/images/guide/sd_webui/extra/png_info_view.jpg)

!!!note
    ComfyUI、InvokeAI、NovelAI 等生成的图片也可以查看生图信息，但是要保证图片未被压缩或者被其他图像工具处理过。


## 移除背景
想要人物的背景移除，可以使用 stable-diffusion-webui-rembg 扩展。在 SD WebUI 的后期处理中，在下方启用移除背景，移除背景选择其中一个算法，再点击生成就可以把图片的背景移除。

![remove_background](../../assets/images/guide/sd_webui/extra/remove_background.jpg)

!!!note
    stable-diffusion-webui-rembg 扩展下载：https://github.com/AUTOMATIC1111/stable-diffusion-webui-rembg

如果有生成蒙版的需求，可以使用 PBRemTools 扩展。在精准背景移除工具选项卡中，导入要移除背景的图片，在后期处理的选项中点击启用，再点提交，这样就可以生成一张移除背景的图片和蒙版。

![rm_background_and_make_mask](../../assets/images/guide/sd_webui/extra/rm_background_and_make_mask.jpg)

!!!note
    PBRemTools 扩展下载：https://github.com/mattyamonaca/PBRemTools


## 图片处理
a1111-sd-webui-haku-img 扩展可对图像进行一些处理，如提取图片线稿，图片像素化等。

![haku_img](../../assets/images/guide/sd_webui/extra/haku_img.jpg)

!!!note
    a1111-sd-webui-haku-img 扩展下载：https://github.com/KohakuBlueleaf/a1111-sd-webui-haku-img


## 面部修复
在 SD WebUI 1.6 之后，官方将自带的面部修复移除了，因为效果过差，而 adetailer 扩展可作为替代品。在文生图或者图生图左下角中可以看到该扩展的选项卡，勾选后即可启用面部修复。

![adetailer](../../assets/images/guide/sd_webui/extra/adetailer.jpg)

注意，在图生图的局部重绘中该扩展并不会生效，因为这个扩展的本质是自动检测面部位置并进行局部重绘。

!!!note
    adetailer 扩展下载：https://github.com/Bing-su/adetailer


## 恢复保存预设的按钮
SD WebUI 1.6 移除了保存提示词预设按钮，所以只能在生成按钮旁边的画笔按钮来保存预设。可以通过 sd-webui-boomer 扩展来恢复这个按钮。

!!!note
    sd-webui-boomer 扩展下载：https://github.com/Haoming02/sd-webui-boomer


## 图片浏览
sd-webui-infinite-image-browsing 扩展作为图片浏览器非常方便。

![infinite_image_browsing](../../assets/images/guide/sd_webui/extra/infinite_image_browsing.jpg)

!!!note
    sd-webui-infinite-image-browsing 扩展下载：https://github.com/zanllp/sd-webui-infinite-image-browsing


## 查找并删除模型里的垃圾数据
SD 1.5 的模型用于生图时只有 2 GB 是有效的数据，但是有许多 SD 1.5 的模型的大小超过了 2 GB。可以通过 stable-diffusion-webui-model-toolkit 扩展查看模型是否有垃圾数据存在。

![search_model_junk_data](../../assets/images/guide/sd_webui/extra/search_model_junk_data.jpg)

如果模型里有垃圾数据，可以通过 sd-webui-model-converter 扩展删除垃圾数据。在模型转换选项卡中，选择要删除垃圾数据的模型，选择删除 EMA 权重，勾选删除已知垃圾数据，点击运行即可删除模型垃圾数据。

![remove_model_junk_data](../../assets/images/guide/sd_webui/extra/remove_model_junk_data.jpg)

有关模型垃圾数据的哔哩哔哩专栏：[【AI绘画】模型修剪教程：8G模型顶级精细？全是垃圾！嘲笑他人命运，尊重他人命运 - 哔哩哔哩](https://www.bilibili.com/read/cv26279169)

!!!note
    stable-diffusion-webui-model-toolkit 扩展下载：https://github.com/arenasys/stable-diffusion-webui-model-toolkit  
    sd-webui-model-converter 扩展下载：https://github.com/Akegarasu/sd-webui-model-converter


## 模型融合
想要模型融合，就用 sd-webui-supermerger 扩展，不过融模虽然容易，但是要融出一个好模并不简单。

!!!note
    sd-webui-supermerger 扩展下载：https://github.com/hako-mikan/sd-webui-supermerger


## 随机抽卡
如果对提示词不熟悉，但又想抽出比较好的图，可以试试 z-a1111-sd-webui-dtg 扩展，启用后就可以快乐的抽卡了。

![dtg](../../assets/images/guide/sd_webui/extra/dtg.jpg)

!!!note
    z-a1111-sd-webui-dtg 扩展下载：https://github.com/KohakuBlueleaf/z-a1111-sd-webui-dtg


## 视频生成
用 AI 来生成视频大致分为两类，一种是视频转绘，另一种是直接生成视频，推荐 ebsynth_utility 扩展和 sd-webui-animatediff 扩展。

!!!note
    ebsynth_utility 扩展下载：https://github.com/s9roll7/ebsynth_utility  
    sd-webui-animatediff 扩展下载：https://github.com/continue-revolution/sd-webui-animatediff


## 低显存跑 SDXL 模型
在 SD WebUI 1.8 中支持了 FP8 权重，可以大大降低 SDXL 模型对显存的占用，最低 6 GB显存即可运行 SDXL 模型。  
启用 FP8 前需要 PyTorch 版本大于 2.1，SD WebUI 版本大于或等于 1.8。  
在 SD WebUI 的`设置`->`优化设置`->`FP8 权重`，选择对 SDXL 模型启用，保存设置后即可启用。


## 无限生成图片
右键 SD WebUI 的生成按钮即可看到无限生成 / 停止无限生成的按钮，

![infinite_generate](../../assets/images/guide/sd_webui/extra/infinite_generate.jpg)


## 使用 SDXL 模型时特定的提示词组会出现鬼图
这个可能和提示词权重有关，在 SD WebUI 的`设置`->`SD`->`强调模式`，选择 No norm 后保存设置，使用 SDXL 模型时非常推荐使用 No norm。


## SD WebUI 的 LoRA / Embedding 模型展示的规则
在 SD WebUI 1.8 后，引入了模型的防呆机制，防止用户错误地使用不对应版本的 LoRA / Embedding 模型，导致报错或者出鬼图。防呆机制的规则如下：

1. 当加载了 SD 1.5 的大模型时，只显示适用于 SD 1.5 的 LoRA / Embedding 模型
2. 当加载了 SDXL 的大模型：只显示适用于 SDXL 的 LoRA / Embedding 模型

如果要使用适用于 SD 1.5 的 LoRA / Embedding 模型，只需要将大模型切换成 SD 1.5 的，这时候在 SD WebUI 的模型列表中就可以看到 SD 1.5 的 LoRA / Embedding 模型了，要使用 SDXL 的也同理。

如果要关闭这个防呆机制，可以在 SD WebUI 的`设置`->`扩展模型`，将`在 Lora 页面保持显示所有模型 (否则, 将隐藏不兼容当前加载的 Stable Diffusion 模型版本的模型)`选项勾上，并保存 SD WebUI 的设置。


## 使用 X/Y/Z 图
如果要对提示词、不同模型、参数等坐对比测试时，可以使用 SD WebUI 的 X/Y/Z 图，在 SD WebUI 左下角的脚本中选择 X/Y/Z Plot 即可使用。

下面举个测试不同提示词和提示词引导系数（CFG Scale）的例子。

- 使用的提示词
```
1girl,(loli:1.2),vampire,silver hair,very long hair,two side up,bat hair ornament,bangs,red eyes,light smile,closed mouth,blush,flat chest,gothic lolita,long sleeves,frills,
looking at viewer,heart hands,
simple background,white background,detail light,chromatic_aberration,sunlight,
close up,upper body,
```

- X/Y/Z 图的参数

![xyz_plot_config](../../assets/images/guide/sd_webui/extra/xyz_plot_config.jpg)

Prompr S/R 为提示词替换，这里我填的是`heart hands,"hand on own chin, index finger raised",hand on own chest`，SD WebUI 将第一个逗号前的提示词作为被替换的对象（也就是`heart hands`），生图时将所写的完整提示词中的`heart hands`替换成`heart hands`、`hand on own chin, index finger raised`、`hand on own chest`。

CFG Scale 为提示词引导系数，在 SD WebUI 的生图参数调整界面中可以看到该选项，生图时将依次设置该值为`7`和`5`。

生图完成后将会得到下面的 X/Y/Z 图。

![xyz_plot](../../assets/images/guide/sd_webui/extra/xyz_plot.jpg)

!!!note
    关于 X/Y/Z 图的说明可参看：[Features · AUTOMATIC1111/stable-diffusion-webui Wiki](https://github.com/AUTOMATIC1111/stable-diffusion-webui/wiki/Features#xyz-plot)


## 为 SD WebUI 模型列表中的模型添加预览图
模型在放置在 SD WebUI 的模型目录后，在 SD WebUI 的模型列表中看到模型并没有预览图。

![no_preview_image_for_model](../../assets/images/guide/sd_webui/extra/no_preview_image_for_model.jpg)

这里有几种方法为模型添加模型预览图：

- 方法 1：使用 SD WebUI 的模型管理功能。

生成一张用于添加模型预览图的图片。

![generate_image_for_model_preview_image](../../assets/images/guide/sd_webui/extra/generate_image_for_model_preview_image.jpg)

在 SD WebUI 的模型列表找到要添加模型预览图的模型，并点击右上角的设置图标。

![open_model_info_interface](../../assets/images/guide/sd_webui/extra/open_model_info_interface.jpg)

在模型信息页面点击下方的替换预览图像，这时模型就有了预览图。

![replace_model_preview_image](../../assets/images/guide/sd_webui/extra/replace_model_preview_image.jpg)

- 方法 2：手动将图片命名成和模型一样的并放至在和模型同一个目录下。

将一张图片的文件名命名成和模型一样的名字，然后放在和模型文件放在一起即可。

![rename_image_file_name_and_put_into_model_folder](../../assets/images/guide/sd_webui/extra/rename_image_file_name_and_put_into_model_folder.jpg)

- 方法 3：使用扩展（不推荐）。

可以使用的扩展有 [Stable-Diffusion-Webui-Civitai-Helper](https://github.com/butaixianran/Stable-Diffusion-Webui-Civitai-Helper)、[sd-civitai-browser-plus](https://github.com/BlafKing/sd-civitai-browser-plus)，这里就不做详细的介绍了。


## 启用 / 禁用共享显存
在 Nvidia 显卡驱动大于 525 后，允许 SD WebUI 等基于 SD 的软件调用显卡的共享显存，以弥补显卡的专用显存不足的问题。但是在 SD WebUI 调用共享显存后，出图的速度会大大降低，所以可以禁用共享显存来防止这种情况。

!!!note
    在禁用共享显存之前，请确保 Nvidia 显卡驱动的版本大于 536。

- 使用绘世启动器禁用

在绘世启动器的`高级选项`中，`性能设置`一栏有个`使用共享显存`的开关，关闭后即可禁用共享显存。

- 使用 Nvidia 显卡驱动面板

参考 Nvidia 官方文档：https://nvidia.custhelp.com/app/answers/detail/a_id/5490


## 保存 SD WebUI 预设
如果需要在进入 SD WebUI 后自动应用之前的参数，可以将这些参数调整好（建议先刷新一遍 SD WebUI 的网页），然后在 SD WebUI 的`设置`->`默认设置`，点击`应用`将这些参数保存到预设中，这些预设将保存在 ui-config.json 文件中，当点击`重载 UI`后预设将生效。

如果想重置预设，可以在 SD WebUI 的目录下把 ui-config.json 文件删除，并重启 SD WebUI。


## 将当前的生图参数保存成工作流
在 SD WebUI 中可以通过安装 LightDiffusionFlow 扩展实现 ComfyUI 的保存工作流的效果，生图调整好后，在 SD WebUI 右下角看到该扩展的选项卡，点击保存按钮即可将当前的所有生图参数保存在一个工作流文件中。更多的工作流可在该网站查看：https://www.lightflow.ai

!!!note
    LightDiffusionFlow 扩展下载：https://github.com/Tencent/LightDiffusionFlow


## 为提示词补全扩展添加词库和中文翻译
[a1111-sd-webui-tagcomplete](https://github.com/DominikDoom/a1111-sd-webui-tagcomplete) 扩展可以提供提示词补全功能，在 SD WebUI 设置中和该扩展有关的设置中可以更换提示词补全的词库，也可以添加中文翻译，下面是更全的提示词补全词库和对应的中文翻译的下载地址。

[Tag++ 下载](https://modelscope.cn/models/licyks/sdnote/resolve/master/tag/tags%2B%2B.zip)

将这个文件下载到本地并解压后，放进`stable-diffusion-webui/extensions/a1111-sd-webui-tagcomplete/tags`文件夹中，然后在 SD WebUI 的`设置`->`标签自动补全`中，在`选择使用的标签文件名`选择`tag++.csv`，`翻译文件名`选择`tag++_zh_new.csv`，再点击上方的保存设置使设置生效。

![switch_tag_file_and_add_tag_translation_for_tagcomplete](../../assets/images/guide/sd_webui/extra/switch_tag_file_and_add_tag_translation_for_tagcomplete.jpg)

这样不仅可以看补全的提示词对应的翻译，也可以使用中文来触发提示词补全。


## 图生图回送
在图生图界面中，除了可以通过手动发送图生图的结果回图生图界面再进行图生图，还可以通过图生图界面的回送脚本自动进行这个过程。

![lookback_script](../../assets/images/guide/sd_webui/extra/lookback_script.png)


## 提示词矩阵
在 SD WebUI 界面的左下角脚本中，选择 Prompt matrix 即可启用提示词矩阵。

![prompt_matrix_script](../../assets/images/guide/sd_webui/extra/prompt_matrix_script.png)

该脚本的功能类似 X/Y/Z 脚本中的 Prompt S/R 功能，通过分隔符对提示词进行组合。

下面是一段使用提示词矩阵的提示词。

```
1girl,solo,cherry blossoms,hair flower,pink flower,hair ribbon,cat ears,animal ear fluff,grey hair,short hair,bangs,blue eyes,hair between eyes,eyebrows visible through hair,blush,neck ribbon,white dress,frilled collar,medium dress,petticoat,detached sleeves,flat chest,
couch,indoors,room,desk,vase,flower,
front view,<lora:ill-xl-01-mmafu_1-000030:1>,
holding pillow,pillow hug,sitting,on couch,looking at viewer,| open mouth,wavy mouth,| tears,teardrop,streaming tears,
```

!!!note
    提示词中的 \<lora:ill-xl-01-mmafu_1-000030:1\> 为画风 LoRA，用于调整画风：[ill-xl-01-mmafu_1-000030.safetensors](https://modelscope.cn/models/licyks/sd-lora/resolve/master/sdxl/style/ill-xl-01-mmafu_1-000030.safetensors)[(Civitai)](https://civitai.com/models/980505/artist-style)。

提示词矩阵脚本根据`|`符号对提示词划分，此时最终会得到 4 组提示词。

提示词组 1：
```
1girl,solo,cherry blossoms,hair flower,pink flower,hair ribbon,cat ears,animal ear fluff,grey hair,short hair,bangs,blue eyes,hair between eyes,eyebrows visible through hair,blush,neck ribbon,white dress,frilled collar,medium dress,petticoat,detached sleeves,flat chest,
couch,indoors,room,desk,vase,flower,
front view,<lora:ill-xl-01-mmafu_1-000030:1>,
holding pillow,pillow hug,sitting,on couch,looking at viewer,
```

提示词组 2：

```
1girl,solo,cherry blossoms,hair flower,pink flower,hair ribbon,cat ears,animal ear fluff,grey hair,short hair,bangs,blue eyes,hair between eyes,eyebrows visible through hair,blush,neck ribbon,white dress,frilled collar,medium dress,petticoat,detached sleeves,flat chest,
couch,indoors,room,desk,vase,flower,
front view,<lora:ill-xl-01-mmafu_1-000030:1>,
holding pillow,pillow hug,sitting,on couch,looking at viewer,, open mouth,wavy mouth, 
```

提示词组 3：

```
1girl,solo,cherry blossoms,hair flower,pink flower,hair ribbon,cat ears,animal ear fluff,grey hair,short hair,bangs,blue eyes,hair between eyes,eyebrows visible through hair,blush,neck ribbon,white dress,frilled collar,medium dress,petticoat,detached sleeves,flat chest,
couch,indoors,room,desk,vase,flower,
front view,<lora:ill-xl-01-mmafu_1-000030:1>,
holding pillow,pillow hug,sitting,on couch,looking at viewer,, tears,teardrop,streaming tears, 
```

提示词组 4：

```
1girl,solo,cherry blossoms,hair flower,pink flower,hair ribbon,cat ears,animal ear fluff,grey hair,short hair,bangs,blue eyes,hair between eyes,eyebrows visible through hair,blush,neck ribbon,white dress,frilled collar,medium dress,petticoat,detached sleeves,flat chest,
couch,indoors,room,desk,vase,flower,
front view,<lora:ill-xl-01-mmafu_1-000030:1>,
holding pillow,pillow hug,sitting,on couch,looking at viewer,, open mouth,wavy mouth, tears,teardrop,streaming tears, 
```

现在对这 4 组提示词简化一下，得到变化的部分。

- `holding pillow,pillow hug,sitting,on couch,looking at viewer,`
- `holding pillow,pillow hug,sitting,on couch,looking at viewer,, open mouth,wavy mouth, `
- `holding pillow,pillow hug,sitting,on couch,looking at viewer,, tears,teardrop,streaming tears, `
- `holding pillow,pillow hug,sitting,on couch,looking at viewer,, open mouth,wavy mouth, tears,teardrop,streaming tears, `

这就是提示词矩阵根据`|`符号对提示词的分割得到的提示词变化，最后的得到的图片如下。

![use_prompt_matrix_script](../../assets/images/guide/sd_webui/extra/use_prompt_matrix_script.png)

可以通过提示词矩阵简单制作提示词的对比图。


## 在图生图和高分辨率修复使用额外噪声
该选项可以在 SD WebUI 的**设置 -> 图生图 -> 图生图和高分辨率修复的额外噪声倍率**找到，为了便于调整，可以在**设置 -> UI 便捷设置**中，在**文生图设置项**和**图生图设置项**中添加 img2img_extra_noise 这个选项，并保存 SD WebUI 设置。

该选项默认为 0，如果要设置，通常需要结合重绘幅度进行调整，该值需要小于重绘幅度的值。

通过额外的噪声，可以在高分辨率修复或者图生图中为图片添加更多的细节。

下面的图片在图生图中进行放大，放大算法使用 R-ESRGAN 4x+ Anime6B，重绘幅度 设置为 0.4。

|额外噪声倍率|0|0.1|
|---|---|---|
|效果图|![img2img_to_upscale_without_extra_noise](../../assets/images/guide/sd_webui/extra/img2img_to_upscale_without_extra_noise.png)|![img2img_to_upscale_with_extra_noise](../../assets/images/guide/sd_webui/extra/img2img_to_upscale_with_extra_noise.png)|

可以看到使用额外噪声后图片细节有了增加，但该值较高的时候可能会导致细节过多使画面变脏。


## 直出高分辨率图
通常情况下，想要直出超出原图训练分辨率的图片可能会造成图片崩坏，比如使用 SDXL 模型（通常使用 1024x1024 的分辨率进行训练）直出 1920x1080 的图时，可能就会出现图片崩坏的情况，此时就可以通过 sd-webui-kohya-hiresfix 扩展解决。

!!!note
    sd-webui-kohya-hiresfix 扩展下载：https://github.com/w-e-w/sd-webui-kohya-hiresfix

安装该扩展后，在 SD WebUI 左下角可以看到 Kohya Hires.fix 选项，通常启用后使用默认参数就有比较好的效果，可自行尝试调整参数以达到更好的效果。

|禁用 Kohya Hires.fix|启用 Kohya Hires.fix|
|---|---|
|![generate_high_resolution_without_kohya_hires](../../assets/images/guide/sd_webui/extra/generate_high_resolution_without_kohya_hires.png)|![generate_high_resolution_with_kohya_hires](../../assets/images/guide/sd_webui/extra/generate_high_resolution_with_kohya_hires.png)|

!!!note
    Kohya HRFix 实现源码：[SDXLで高解像度での構図の破綻を軽減する](https://gist.github.com/kohya-ss/3f774da220df102548093a7abc8538ed)


## 使用动态提示词引导系数
该扩展用于设置动态提示词引导系数，可使在较高的提示词引导系数下颜色能够保持正常。

下面提供一个预设值可供参考。

|选项|值|
|---|---|
|Mimic Scale|5|
|Threshold Percentile|95|
|Mimic Mode|Half Cosine Up|
|Mimic Scale Min|4|
|Cfg Mode|Half Cosine Up|
|Cfg Scale Min|4|
|Sched Val|4|
|Separate Feature Channels|启用|
|Scaling Startpoint|MEAN|
|Variability Measure|AD|
|Interpolate Phi|1|

启用后，可以避免高提示词引导系数下颜色异常。

|提示词引导系数|5|15（启用 DynamicThresholding）|15|
|---|---|---|---|
|效果图|![use_cfg_5_without_dynamic_cfg](../../assets/images/guide/sd_webui/extra/use_cfg_5_without_dynamic_cfg.png)|![use_cfg_15_without_dynamic_cfg](../../assets/images/guide/sd_webui/extra/use_cfg_15_without_dynamic_cfg.png)|![use_cfg_15_with_dynamic_cfg](../../assets/images/guide/sd_webui/extra/use_cfg_15_with_dynamic_cfg.png)|

!!!note
    DynamicThresholding 相关的说明：[mcmonkeyprojects/sd-dynamic-thresholding Wiki](https://github.com/mcmonkeyprojects/sd-dynamic-thresholding/wiki)


## 监测跑图时硬件的占用情况
如果想在跑图的时候快捷查看硬件的占用信息，如显存占用等，可以安装 sd-webui-resource-monitor 扩展，安装后在 SD WebUI 的右上角就可以看到硬件的占用信息。

![use_resource_monitor](../../assets/images/guide/sd_webui/extra/use_resource_monitor.png)

!!!note
    1. sd-webui-resource-monitor 扩展下载：https://github.com/Haoming02/sd-webui-resource-monitor  
    2. 该扩展可能会导致 [sd-webui-weight-helper](https://github.com/nihedon/sd-webui-weight-helper) 扩展无法正常显示界面，如果出现该情况请禁用该扩展。


## 固定出图分辨率的宽高比
调整出图的分辨率时，如果想要保持当前的宽高比不变，可以安装 sd-webui-aspect-ratio-helper 扩展，安装后在调整宽度和高度的选项旁边可以看到一个`Off`按钮，点开后可以看到`Off`、🔒和一些宽高比预设。

选择🔒后，当调整其中一个分辨率的值时，sd-webui-aspect-ratio-helper 扩展将根据原来的宽高比自动调整另一个分辨率的值。

选择宽高比预设也是一样的效果。如果要添加宽高比预设，可以在 SD WebUI 的**设置 -> 纵横比助手 -> 前端纵横比按钮**选项中修改。

!!!note
    sd-webui-aspect-ratio-helper 扩展下载：https://github.com/thomasasfk/sd-webui-aspect-ratio-helper

