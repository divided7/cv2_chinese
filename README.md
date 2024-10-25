# cv2_chinese
以下demo能直接替换cv2.putText,
插入函数后,将原本的代码 `cv2.putText(img, ...)` 替换为 `img = putText(img, ...)`

```python
import cv2
import numpy as np
from PIL import Image, ImageDraw, ImageFont


def putText(img, text, position, ziti, font_size, color, cuxi, aa):
    # 将OpenCV图像转换为Pillow图像
    font_size = int(font_size*35)
    position = (position[0], position[1] - 25)

    img_pil = Image.fromarray(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))

    # 创建一个绘图对象
    draw = ImageDraw.Draw(img_pil)

    # 加载字体
    font = ImageFont.truetype("/usr/share/fonts/truetype/chinese/simhei.ttf", font_size)

    # 在Pillow图像上绘制中文
    draw.text(position, text, font=font, fill=color)

    # 将Pillow图像转换回OpenCV图像
    img = cv2.cvtColor(np.array(img_pil), cv2.COLOR_RGB2BGR)

    return img


# 示例用法
if __name__ == "__main__":
    # 创建一个空白图像
    info_frame = np.ones((540, 960, 3), dtype=np.uint8) * 255

    cv2.putText(info_frame, f"STATE: grab the bar, grip width score:  ", (100, 50),
                cv2.FONT_HERSHEY_SIMPLEX, 1.0, (0, 0, 0), 2,
                cv2.LINE_AA)

    cv2.putText(info_frame, f"aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa", (100, 100),
                cv2.FONT_HERSHEY_SIMPLEX, 1.0, (0, 0, 0), 2,
                cv2.LINE_AA)


    info_frame = putText(info_frame, f"STATE: grab the bar, grip width score:  ", (100, 50),
            cv2.FONT_HERSHEY_SIMPLEX, 1.0, (0, 0, 255), 2,
            cv2.LINE_AA)

    info_frame = putText(info_frame, f"啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊啊 ", (100, 100),
            cv2.FONT_HERSHEY_SIMPLEX, 1.0, (0, 0, 255), 2,
            cv2.LINE_AA)
    # 保存图片
    cv2.imwrite('output_with_chinese_text.png', info_frame)

```
