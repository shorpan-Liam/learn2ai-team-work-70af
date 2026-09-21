# React 状态与事件

## 学习目标

- 使用 `useState` 保存界面状态。
- 响应点击和输入事件。
- 根据状态派生和渲染不同内容。

## 1. 状态是什么

普通变量改变后不会自动触发组件重新渲染。需要反映在界面上的可变数据，应使用状态。

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <button type="button" onClick={() => setCount(count + 1)}>
      已点击 {count} 次
    </button>
  );
}
```

`useState` 返回当前值和更新函数。不要直接修改状态，而应调用更新函数。

## 2. 处理输入

受控输入框的值来自状态，并通过 `onChange` 更新状态。

```jsx
function SearchBox() {
  const [query, setQuery] = useState("");

  return (
    <label>
      搜索课程
      <input
        value={query}
        onChange={(event) => setQuery(event.target.value)}
        placeholder="输入关键词"
      />
    </label>
  );
}
```

## 3. 根据状态筛选列表

能由现有 props 或状态计算出的值通常不需要再保存为状态。

```jsx
const visibleCourses = courses.filter((course) =>
  course.title.toLowerCase().includes(query.trim().toLowerCase()),
);
```

这种写法让数据来源保持唯一，避免原列表、关键词和筛选结果不同步。

## 4. 条件渲染

可以使用三元表达式、逻辑与运算符或提前返回：

```jsx
{visibleCourses.length > 0 ? (
  <CourseList courses={visibleCourses} />
) : (
  <p role="status">没有匹配的课程</p>
)}
```

## 5. 状态设计原则

- 只保存界面真正需要记住的最少数据。
- 状态放在需要共同使用它的组件的最近共同父组件中。
- 更新依赖旧值时使用函数形式：`setCount((current) => current + 1)`。
- 不要直接修改数组或对象；使用 `map`、`filter`、展开语法创建新值。

## 自查

1. 搜索关键词是否由状态控制？
2. 清空关键词后，完整列表是否恢复？
3. 搜索无结果时，用户是否得到明确提示？
