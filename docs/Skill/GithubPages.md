# github pages
## 在github pages上渲染tex
**暂行方法**:  
实在不想配置hexo,也没有设置主题文件,目前暂时使用的方法是在 **_config.yml** 中添加:
```json
markdown: kramdown
```
然后在每一个需要tex数学公式的markdown文件前添加加上官方提供的脚本链接:  

```html
<head>
    <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
    <script type="text/x-mathjax-config">
        MathJax.Hub.Config({
            tex2jax: {
            skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
            inlineMath: [['$','$'],["\\(","\\)"]],
            displayMath: [
                ['$$', '$$'],
                ['\\[', '\\]']
                ],
            }
        });
    </script>
</head>
```