hunyuan-video-gallery-without-prompt

本人近期在图片和视频生成均改用Hunyuan Video，考虑到分辨率不同以及要展示图片和视频内容就新建了项目。经测试能正常生成的最大分辨率约为1584x896，本项目中的图片和视频也使用这个分辨率，视频长度为21帧，帧率12fps。竖屏内容可用的最大分辨率为540x960，垂直分辨率相比横屏没有明显提升，出片率也较低。由于这个分辨率不明显高于streamlit的缩略图分辨率，相比之前的项目在页面上取消了下载按钮已提高外观一致性。由于Hunyuan Video在使用单个风格提示词时引导效果一般且无提示词基本不影响出片率，本项目取消风格选择。

由于实现流程可能较为复杂，本项目未添加预期的刷新按钮返回页面顶部以及翻页按钮功能（在页面顶部重新选中随机选项可以实现刷新，刷新网页会回到默认选项）。视频自动播放功能有一定问题，应该是库文件造成的。

本项目的媒体文件尚未完成上传。

本项目已部署到Streamlit Cloud，域名为https://william7004-hunyuan-video-gallery-without-prompt.streamlit.app

本地部署流程

建议使用Python=3.10环境

1.安装依赖
```bash
pip install -r requirements.txt
```
2.运行应用
```bash
streamlit run streamlit_app.py
```
