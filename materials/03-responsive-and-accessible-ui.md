# 响应式与可访问的 React 页面

## 学习目标

- 使用现代 CSS 构建响应式布局。
- 编写语义化、键盘可操作的页面。
- 为常见交互提供清晰反馈。

## 1. 从语义结构开始

优先使用表达内容含义的 HTML 元素：

```jsx
function App() {
  return (
    <>
      <header>{/* 品牌与导航 */}</header>
      <main>
        <section aria-labelledby="featured-title">
          <h2 id="featured-title">推荐课程</h2>
        </section>
      </main>
      <footer>{/* 版权与联系信息 */}</footer>
    </>
  );
}
```

页面应有一个清晰的 `h1`，后续标题按层级组织。真正执行操作时使用 `button`，跳转到地址时使用 `a`。

## 2. 响应式布局

Grid 很适合卡片列表：

```css
.course-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(100%, 16rem), 1fr));
  gap: 1rem;
}
```

页面主体应设置合理的最大宽度和边距：

```css
.page-shell {
  width: min(100% - 2rem, 72rem);
  margin-inline: auto;
}
```

至少检查 375px 手机宽度和 1280px 桌面宽度。不要依赖固定像素宽度撑开页面。

## 3. 键盘与焦点

交互控件必须可以使用 Tab 键访问，并具有清晰焦点样式。

```css
:focus-visible {
  outline: 3px solid #2563eb;
  outline-offset: 3px;
}
```

不要移除焦点轮廓，除非提供同等清晰的替代样式。只显示图标的按钮需要可访问名称，例如 `aria-label="清空搜索"`。

## 4. 颜色和反馈

- 正文与背景应有足够对比度。
- 不要只用颜色表达状态，同时提供文字或图标。
- 按钮应有默认、悬停、焦点和禁用状态。
- 图片需要有意义的 `alt`；纯装饰图片使用空的 `alt=""`。

## 5. 基础质量检查

完成页面后执行：

```bash
npm run build
npm run lint
```

同时手动验证：

- 页面在手机和桌面宽度下没有横向滚动或内容重叠。
- 所有按钮和输入框都能通过键盘操作。
- 搜索有结果、无结果和清空三种状态均正确。
- 浏览器控制台没有 React 警告或运行时错误。
