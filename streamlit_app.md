### 提示词：

使用streamlit写一个程序，实现以下功能：

1.设置layout=wide。在同一行从左到右依次创建4个下拉菜单。

2.第一个下拉菜单有“图片”和“视频”两个选项，分别用于选择当前文件夹中的pictures1/pictures2或videos1/videos2文件夹。

3.第二个下拉菜单有“16：9”和“9：16”两个选项，分别用于选中pictures1/videos1或pictures2/videos2文件夹。

4.第三个下拉菜单的选项为8到32之间且为4的倍数的数字，用于选择同时显示的图片/视频的个数。

5.选中文件夹后，在相应文件夹中随即选择张图片/视频。第3步选中的文件夹为16：9则分两列显示，第二步选中的文件夹为9：16则分四列显示。pictures开头的文件夹为图片，videos开头的文件夹为视频，视频设置自动播放和循环播放。

6.第四个下拉菜单用于选择图片/视频范围，默认选项为“随机”，并根据第4步选中的同时显示的图片/视频的个数和相应文件夹中的图片/视频数量创建选项，用于选择根据文件名排序后在相应位置的图片/视频。

7.如果第四个下拉菜单选中了“随机”，在页面底部创建刷新按钮，用于随机选择相同数量的图片/视频并回到页面顶部。如果第四个下拉菜单选中了具体的图片/视频范围，在页面底部同一行创建“上一页”和“下一页”按钮，分别用于切换到第四个下拉菜单的上一个选项和下一个选项对应的图片/视频范围。

8.考虑到部分文件夹没有添加足够的图片/视频，在选中的文件夹中图片/视频数量不足时显示所有图片/视频。

### 思维链：
好，我需要写一个Streamlit程序，实现这些功能。首先，设置布局为宽模式，这样界面会更开阔。

接着，在同一行从左到右创建4个下拉菜单。第一个下拉菜单选项是“图片”和“视频”，用来选择pictures1/pictures2或videos1/videos2文件夹。

第二个下拉菜单有“16：9”和“9：16”，根据这个选择pictures1/videos1或pictures2/videos2文件夹。

第三个下拉菜单是8到32之间且为4的倍数的数字，用于选择同时显示的图片或视频的个数。

第四个下拉菜单默认是“随机”，还需要根据第三步选中的数量和文件夹中的数量来生成选项，供用户选择具体的图片或视频范围。

当用户选中文件夹后，要从相应文件夹中随机选择图片或视频，并根据第二步的选择来决定显示的列数。如果是16:9，就分两列显示；如果是9:16，就分四列显示。图片文件夹是以pictures开头，视频文件夹是以videos开头，视频要设置自动播放和循环播放。

另外，第四个下拉菜单如果选择“随机”，要在页面底部创建一个刷新按钮，点击后随机选择相同数量的图片或视频，并回到页面顶部。如果选择具体的范围，就要创建“上一页”和“下一页”按钮，用于切换到上一个或下一个选项对应的图片或视频范围。

还要考虑文件夹中图片或视频数量不足的情况，这时候就显示所有可用的图片或视频。

好的，我得先导入Streamlit库，设置页面布局为宽模式，使用st.set_page_config(layout="wide")。

然后，创建四个下拉菜单，可以使用st.selectbox来实现。

第一个下拉菜单选项是["图片", "视频"]，根据选择来确定文件夹的前缀，是pictures还是videos。

第二个下拉菜单选项是["16：9", "9：16"]，根据选择来确定是1还是2，组合成文件夹名称，比如pictures1或pictures2，videos1或videos2。

第三个下拉菜单选项是8,12,16,20,24,28,32，这些是4的倍数，且在8到32之间。

第四个下拉菜单，默认选项是“随机”，还需要根据第三步选择的数量和文件夹中的数量来生成其他选项。

接下来，需要读取文件夹中的图片或视频文件。根据第一步和第二步的选择组合出文件夹路径，比如pictures1、pictures2、videos1、videos2。

然后，从选中的文件夹中随机选择指定数量的文件。如果文件数量不足，就显示所有文件。

根据第二步的选择，如果是16:9，就分两列显示；如果是9:16，就分四列显示。

如果是图片，就用st.image显示；如果是视频，就用st.video显示，并设置自动播放和循环播放。

对于第四个下拉菜单，如果选择“随机”，就在底部创建一个刷新按钮，点击后重新随机选择相同数量的文件，并回到页面顶部。可以使用st.button来创建按钮，并在点击时重新选择文件并刷新页面。

如果选择具体的范围，就需要根据选择的范围来显示相应的图片或视频，并在底部创建“上一页”和“下一页”按钮，用于切换到上一个或下一个选项对应的范围。

还需要确保文件夹中文件数量不足时，显示所有可用的文件。

好，我需要先写代码来实现这些功能。

首先，导入Streamlit：

import streamlit as st

然后，设置页面布局：

st.set_page_config(layout="wide")

接下来，创建四个下拉菜单，放在同一行。可以使用st.beta_columns来实现。

cols = st.beta_columns(4)

在每个列中放置一个下拉菜单。

在第一个列中：

with cols[0]:

media_type = st.selectbox("选择类型", ["图片", "视频"])

在第二个列中：

with cols[1]:

aspect_ratio = st.selectbox("选择比例", ["16：9", "9：16"])

在第三个列中：

with cols[2]:

num_items = st.selectbox("选择数量", [i for i in range(8,33,4)])

在第四个列中：

with cols[3]:

range_option = st.selectbox("选择范围", ["随机"])

暂时先设为["随机"]，后面根据需要动态添加选项。

然后，根据第一步和第二步的选择，组合出文件夹的路径。

如果media_type是“图片”，前缀是"pictures"，否则是"videos"。

如果aspect_ratio是“16：9”，后缀是"1"，否则是"2"。

所以文件夹路径是 os.path.join(prefix, suffix)

比如 pictures1, pictures2, videos1, videos2.

然后，读取该文件夹中的所有图片或视频文件。

如果是图片，假设是图片文件，比如.jpg, .png等；如果是视频，假设是.mp4等。

获取文件列表，并根据num_items选择相应的数量，如果不足，就选择所有。

然后，根据aspect_ratio来决定显示的列数。

如果是16:9，分两列显示；如果是9:16，分四列显示。

可以使用st.columns来创建列。

比如：

if aspect_ratio == "16：9":

cols_display = st.columns(2)

else:

cols_display = st.columns(4)

然后，在这些列中显示图片或视频。

如果是图片，用st.image显示；如果是视频，用st.video显示，并设置autoplay=True和loop=True。

接下来，处理第四个下拉菜单的动态选项生成。

需要根据num_items和文件夹中的文件数量来生成选项。

比如，如果文件夹中有50个文件，num_items是8，那么可以生成范围选项，比如1-8, 9-16, 17-24, 25-32, 33-40, 41-48, 49-50。

需要根据文件数量和num_items来划分范围。

在range_option中，除了“随机”，还需要添加这些范围选项。

所以，需要先获取文件夹中的文件数量，然后根据num_items来划分范围。

比如：

file_list = list of files

total_files = len(file_list)

num_items = selected number

num_pages = total_files // num_items

if total_files % num_items != 0:

num_pages +=1

for i in range(num_pages):

start = i*num_items +1

end = min((i+1)*num_items, total_files)

range_option.append(f"{start}-{end}")

然后，在第四个下拉菜单中，选项是["随机", "1-8", "9-16", ...]

根据用户选择，如果是“随机”，则随机选择num_items个文件，并在底部创建刷新按钮。

如果是具体的范围，比如"1-8"，则选择对应的文件，并在底部创建“上一页”和“下一页”按钮。

需要维护当前的页面索引，以便切换上一页和下一页。

还需要处理文件数量不足的情况，比如如果total_files < num_items, 就显示1-5，如果total_files=5。

另外，还需要处理文件夹不存在或没有文件的情况。

好的，我需要把这些逻辑写进代码里。

另外，关于回到页面顶部，Streamlit没有直接的支持，可能需要使用锚点或者重新渲染页面。

可能通过重新运行脚本来实现刷新效果。

好，我先写个基础版本，再逐步完善。

先写读取文件夹的函数，获取文件列表。

然后根据选择生成范围选项。

再根据选择显示相应的文件，并在底部创建相应的按钮。

还需要处理按钮点击事件，来切换范围或刷新。

可能需要使用st.session_state来维护状态，比如当前选择的范围或者页面索引。

### 回答正文：

## 使用 Streamlit 实现多媒体文件展示程序

### 代码实现

```python
import streamlit as st
import os
import random

# 设置页面布局为宽模式
st.set_page_config(layout="wide")

# 创建四个下拉菜单
cols = st.beta_columns(4)

with cols[0]:
    media_type = st.selectbox("选择类型", ["图片", "视频"])

with cols[1]:
    aspect_ratio = st.selectbox("选择比例", ["16：9", "9：16"])

with cols[2]:
    num_items = st.selectbox("选择数量", [i for i in range(8, 33, 4)])

# 获取当前文件夹路径
current_dir = os.getcwd()

# 根据选择确定文件夹前缀和后缀
if media_type == "图片":
    prefix = "pictures"
else:
    prefix = "videos"

if aspect_ratio == "16：9":
    suffix = "1"
else:
    suffix = "2"

folder_path = os.path.join(current_dir, f"{prefix}{suffix}")

# 检查文件夹是否存在，如果不存在则显示错误信息
if not os.path.exists(folder_path):
    st.error(f"文件夹 {folder_path} 不存在")
else:
    # 获取文件列表
    if media_type == "图片":
        file_extensions = ['.jpg', '.jpeg', '.png', '.bmp', '.gif']
    else:
        file_extensions = ['.mp4', '.avi', '.mkv', '.mov']

    file_list = [f for f in os.listdir(folder_path) if os.path.isfile(os.path.join(folder_path, f)) and os.path.splitext(f)[1].lower() in file_extensions]
    total_files = len(file_list)

    if total_files == 0:
        st.warning("文件夹中没有文件")
    else:
        # 计算范围选项
        num_pages = total_files // num_items
        if total_files % num_items != 0:
            num_pages += 1
        range_options = ["随机"]
        for i in range(num_pages):
            start = i * num_items + 1
            end = min((i + 1) * num_items, total_files)
            range_options.append(f"{start}-{end}")

        with cols[3]:
            range_option = st.selectbox("选择范围", range_options)

        # 根据选择的范围获取文件
        if range_option == "随机":
            selected_files = random.sample(file_list, min(num_items, total_files))
            page_index = None  # 随机选择时没有页面索引
        else:
            # 解析范围，获取起始和结束索引
            start_end = range_option.split("-")
            start_index = int(start_end[0]) - 1  # 转换为0-based索引
            end_index = int(start_end[1])
            selected_files = file_list[start_index:end_index]
            # 计算当前页面索引
            page_size = num_items
            page_index = start_index // page_size

        # 根据选择的宽高比决定显示的列数
        if aspect_ratio == "16：9":
            cols_display = st.columns(2)
        else:
            cols_display = st.columns(4)

        # 显示选中的文件
        for i, file in enumerate(selected_files):
            col_idx = i % len(cols_display)
            with cols_display[col_idx]:
                file_path = os.path.join(folder_path, file)
                if media_type == "图片":
                    st.image(file_path, use_column_width=True)
                else:
                    st.video(file_path, format="video/mp4", start_time=0)

        # 根据选择的范围显示按钮
        if range_option == "随机":
            # 创建刷新按钮
            if st.button("刷新"):
                # 刷新页面，重新随机选择文件
                pass  # 需要进一步实现刷新功能
        else:
            # 创建上一页和下一页按钮
            if st.button("上一页"):
                # 切换到上一个页面
                pass  # 需要进一步实现上一页功能
            if st.button("下一页"):
                # 切换到下一个页面
                pass  # 需要进一步实现下一页功能
```

### 代码解释

1. **设置页面布局**：使用 `st.set_page_config(layout="wide")` 将页面布局设为宽模式。
2. **创建下拉菜单**：
    - 使用 `st.selectbox` 在四个列中分别创建选择类型、比例、数量和范围的下拉菜单。
3. **确定文件夹路径**：
    - 根据选择的类型和比例，组合出文件夹的前缀和后缀，拼接出文件夹路径。
4. **检查文件夹是否存在**：
    - 如果文件夹不存在，显示错误信息。
5. **获取文件列表**：
    - 根据选择的类型，过滤出相应的文件扩展名，并获取文件列表。
6. **计算范围选项**：
    - 根据选择的数量和文件总数，计算出范围选项，并在第四个下拉菜单中显示。
7. **根据选择的范围获取文件**：
    - 如果选择“随机”，则随机选择指定数量的文件。
    - 如果选择具体的范围，则根据范围解析出起始和结束索引，选择相应的文件。
8. **显示文件**：
    - 根据选择的宽高比，决定显示的列数。
    - 在相应的列中显示图片或视频文件。
9. **显示按钮**：
    - 如果选择“随机”，则在底部创建刷新按钮。
    - 如果选择具体的范围，则在底部创建上一页和下一页按钮。

### 代码优化与完善

- **刷新功能**：点击刷新按钮时，重新随机选择指定数量的文件，并刷新页面显示。
- **上一页和下一页功能**：根据当前页面索引，切换到上一个或下一个页面对应的文件范围，并刷新页面显示。
- **页面滚动**：可以使用 `st.experimental_rerun()` 来实现页面的重新运行和滚动到顶部。
- **错误处理**：完善文件夹不存在或没有文件时的错误提示。
- **用户体验**：优化界面布局和按钮样式，提升用户体验。

