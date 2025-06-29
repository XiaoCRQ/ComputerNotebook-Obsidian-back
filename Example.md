# Checkbox / Dash / Quote

- [ ] Unchecked Checkbox
- [x] Checked Checkbox
- [-] Todo Checkbox
- Regular List Item

---

> Quote line 1
> Quote line 2

# Note

> [!NOTE]
>
> A regular note
> 
> With a second paragraph

# Tip

> [!TIP]
>
> ```lua
> print('Standard tip')
> ```

# Important

> [!IMPORTANT]
> Exceptional info

# Warning

> [!WARNING] Custom Title
> Dastardly surprise

# Caution

> [!caution]
> Cautionary tale

# Bug

> [!bUg]
> Custom bug

# Heading 1

### Heading 3

#### Heading 4

##### Heading 5

###### Heading 6

![Image](example.png)

```python {filename="demo.py"}
def main() -> None:
    sum = 0
    for i in range(10):
        sum += i
    print(sum)


if __name__ == "__main__":
    main()
```

# LaTeX

$\sqrt{3x-1}+(1+x)^2$

$$
f(x,y) = x + \sqrt{y}
f(x,y) = \sqrt{y} + \frac{x^2}{4y}
$$

# Unordered List

- List Item 1: with [link](https://example.com)

- List Item 2: with `inline` code

  - Nested List 1 Item 1
  - Nested List 1 Item 2
    - Nested List 2 Item 1
      - Nested List 3 Item 1
        - Nested List 4 Item 1

- List Item 3: with [reference link][example]

# Ordered List

1. Item 1
2. Item 2

# Table

| `Left` |   _Center_    | Right | None |
| :----- | :-----------: | ----: | ---- |
| `Code` |   **Bold**    | Plain | Item |
| Item   | [link](/test) |  Item | Item |

[example]: https://example.com

# color

<font face="黑体">我是黑体字</font>
<font face="微软雅黑">我是微软雅黑</font>
<font face="STCAIYUN">我是华文彩云</font>
<font color=red>我是红色</font>
<font color=#008000>我是绿色</font>
<font color=Blue>我是蓝色</font>
<font size=5>我是尺寸</font>
<font face="黑体" color=green size=5>我是黑体，绿色，尺寸为5</font>

<table><tr><td bgcolor=yellow>背景色yellow</td></tr></table>

# font

样式名 效果 Markdown
加粗 文本 **文本** 或 **文本**，用两个_或两个\_包围文本
斜体 文本 _文本_ 或 _文本_，用一个_或一个\_包围文本
删除线 文本 ~~文本~~
下划线 文本 <u>文本</u>，Markdown自身没有实现下划线，但它是HTML的子集，实现了<u>标签
· CSDN的锚和链接是没有下划线的、只是颜色高亮，一般建议加上下划线，会更明确是链接、可点击的；
· 一般文本建议不要加下划线，容易误会成链接
上标 文本上标 文本^上标^
下标 文本下标 文本~下标~
小号字体 小号字体 <small>小号字体</small>
大号字体 大号字体 <big>大号字体</big>
