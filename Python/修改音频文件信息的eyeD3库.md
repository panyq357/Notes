# 修改音频文件信息的eyeD3库

eyeD3库可以用来修改音频文件属性，如艺术家、编号、专辑名等。

## 安装

````powershell
python -m pip install eyed3
````

## 使用

````python
import os
import re
import eyed3

# 脚本和音频文件在同一个文件夹下。
# 这里获取所有音频文件的文件名。
filenames = os.listdir()
for filename in filenames:
    # 从文件名中获取歌曲信息。
    # 该正则表达式匹配这样的歌曲名：“10. title - artist.mp3”。
    num, title, artist = re.search(r"(\d+)\.\s(.*)\s-\s(.*).mp3", filename).groups()

    # 修改歌曲信息。
    audiofile = eyed3.load(filename) # 载入歌曲信息。
    audiofile.tag.artist = artist # 艺术家。
    audiofile.tag.title = title # 标题。
    audiofile.tag.track_num = num # 序号（不是光盘编号）。
    audiofile.tag.save() # 保存。
````

eyeD3库也可用命令行直接调用，具体方法参考[eyeD3的文档](https://eyed3.readthedocs.io/en/latest/)。

## 参考

1. <https://eyed3.readthedocs.io/en/latest/>
