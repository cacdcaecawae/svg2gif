# SVG2GIF

将 SVG 动画转换为 GIF 动画的 Python 工具。

After having a rather niche use case and struggling to find a python convertor for SVG to GIF, this script was written. It is documented that some of the most common open source libraries aren't covering this conversion yet (for good reasons). [reference](https://github.com/ImageMagick/ImageMagick/discussions/2391).

This script takes an SVG file, opens it in Selenium using a Chrome driver, screenshots the svg file in live action, then uses PIL to combine all the saved PNGs to a GIF. There is some smoothing of the GIF by slowing the SVG file to take more screenshots during the animations and then speeding up the GIF to be at the same speed as the original SVG. This can be improved upon. 

Although this framework seems inefficient, there isn't a clean way to "activate" or iterate through animations in an SVG, which is why popular frameworks haven't built a solution to this problem yet.

## 安装依赖

### Python 包

```bash
pip install Pillow beautifulsoup4 selenium
```

或使用 conda：

```bash
conda install -c conda-forge pillow beautifulsoup4 selenium
```

### ChromeDriver

使用 Homebrew 安装（推荐）：

```bash
brew install --cask chromedriver
```

或手动下载：访问 [Chrome for Testing](https://googlechromelabs.github.io/chrome-for-testing/) 下载与您的 Chrome 浏览器版本匹配的 ChromeDriver。

## 使用方法

### 基本用法

```bash
# 使用默认示例文件
python svg2gif.py

# 转换指定的 SVG 文件
python svg2gif.py <svg_file>
```

### 示例

An example [GIF](https://github.com/proselotis/SVG2GIF/blob/main/example/test.gif) and [SVG](https://github.com/proselotis/SVG2GIF/blob/main/example/test.svg) can be seen in the [example folder](https://github.com/proselotis/SVG2GIF/tree/main/example)

## 工作原理

1. 解析 SVG 文件，提取动画时长信息（使用 BeautifulSoup）
2. 使用 Selenium + Chrome 浏览器渲染 SVG 动画
3. 按设定帧率（默认 11 FPS）截取动画帧
4. 使用 Pillow (PIL) 将截图合成为 GIF 文件
5. 自动清理临时文件

## 技术栈

- **Python 3.x**
- **Selenium** - 浏览器自动化
- **Pillow (PIL)** - 图像处理
- **BeautifulSoup4** - SVG 解析
- **Chrome/ChromeDriver** - SVG 渲染

## 注意事项

- 需要安装 Google Chrome 浏览器
- 确保 ChromeDriver 版本与 Chrome 浏览器版本匹配
- 脚本会在当前目录创建临时文件夹 `_screenshots`，运行结束后会自动删除
