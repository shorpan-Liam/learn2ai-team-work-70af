# React 与 JSX 入门

## 学习目标

- 理解 React 组件、JSX 和单向数据流。
- 能使用 Vite 创建并运行 React 项目。
- 能把页面拆成职责清晰的组件。

## 1. 创建项目

需要 Node.js 18 或更高版本。使用 Vite 创建项目：

```bash
npm create vite@latest my-react-app -- --template react
cd my-react-app
npm install
npm run dev
```

常见目录如下：

```text
my-react-app/
├── public/          # 不经过构建处理的静态文件
├── src/
│   ├── assets/      # 图片、字体等资源
│   ├── App.jsx      # 页面根组件
│   ├── App.css
│   └── main.jsx     # 应用入口
├── index.html
└── package.json
```

## 2. 组件

React 组件通常是返回 JSX 的 JavaScript 函数。组件名必须以大写字母开头。

```jsx
function Welcome() {
  return <h1>欢迎学习 React</h1>;
}

export default Welcome;
```

组件应该聚焦单一职责。例如，一个课程页面可以拆成 `Header`、`CourseList`、`CourseCard` 和 `Footer`。

## 3. JSX

JSX 允许在 JavaScript 中描述界面。它接近 HTML，但有几个重要区别：

- 使用 `className`，而不是 `class`。
- JavaScript 表达式写在 `{}` 中。
- 标签必须闭合。
- 一个组件只能返回一个根节点，可使用 Fragment：`<>...</>`。

```jsx
function CourseTitle() {
  const title = "React 前端开发";
  return <h2 className="course-title">{title}</h2>;
}
```

## 4. Props

Props 用于把数据从父组件传给子组件。子组件不应修改收到的 props。

```jsx
function CourseCard({ title, level }) {
  return (
    <article className="course-card">
      <h3>{title}</h3>
      <p>难度：{level}</p>
    </article>
  );
}

function App() {
  return <CourseCard title="React 基础" level="入门" />;
}
```

## 5. 列表渲染

使用 `map` 将数据转换为元素。每个列表项需要稳定、唯一的 `key`。

```jsx
const courses = [
  { id: 1, title: "HTML 与 CSS" },
  { id: 2, title: "React 基础" },
];

function CourseList() {
  return (
    <section>
      {courses.map((course) => (
        <CourseCard key={course.id} title={course.title} />
      ))}
    </section>
  );
}
```

不要使用数组索引作为会增删或排序的列表的 `key`，否则可能出现状态错位。

## 自查

1. 是否能说明组件名为什么要大写？
2. 是否能用 props 复用同一个卡片组件？
3. 是否为列表元素提供了稳定的 `key`？
