# Babel JSX 预设置
通过可配置的 Babel 预设置为 Vue 添加 JSX 支持。 [查看配置项](https://github.com/vuejs/jsx-vue2/tree/dev/packages/babel-preset-jsx)
## 兼容性
* **Babel 7+**。支持 Babel 6，使用 [vuejs/babel-plugin-transform-vue-jsx](https://github.com/vuejs/babel-plugin-transform-vue-jsx)。
* **Vue 2+**。旧版本不支持 JSX。Vue 3 支持使用 [@vue/babel-plugin-jsx](https://github.com/vuejs/babel-plugin-jsx).
## 安装
通过命令行安装：
```shell
npm install @vue/babel-preset-jsx @vue/babel-helper-vue-jsx-merge-props
```
添加预设置到 `babel.config.js`：
```js
module.exports = {
	presets: [
		"@vue/babel-preset-jsx"
	]
}
```
## 语法
### 内容
```jsx
render() {
	return <p>hello</p>
}
```
动态内容
```jsx
render() {
	return <p>hello { this.message }</p>
}
```
自关闭
```jsx
render() {
	return <input />
}
```
组件
```jsx
import MyComponent from './my-component'

export default {
    render() {
        return <MyComponent>hello</MyComponent>
    }
}
```
### 属性
```jsx
render() {
	return <input type="email" />
}
```
动态绑定
```jsx
render() {
	return <input
		type="email"
		placeholder={this.placeholderText}
	/>
}
```
展开运算符（对象需要兼容[ Vue Data Object](https://v2.vuejs.org/v2/guide/render-function.html#The-Data-Object-In-Depth)）
```jsx
render() {
	const inputAttrs = {
		type: 'email',
		placeholder: 'Enter your email'
	}
	return <input
		{...{ attrs: inputAttrs }}
	/>
}
```
### 插槽
命名插槽
```jsx
render() {
	return (
		<MyComponent>
			<header slot="header">header</header>
			<footer slot="footer">footer</footer>
		</MyComponent>
	)
}
```
作用域插槽
```jsx
render() {
	const scopedSlots = {
		header: () => <header>header</header>,
		footer: () => <footer>footer</footer>
	}
	return <MyComponent scopedSlots={scopedSlots}></MyComponent>
}
```
### 指令
```jsx
<input vModel={this.newTodoText} />
```
修饰符
```jsx
<input vModel_trim={this.newTodoText} />
```
参数
```jsx
<input vOn:click={this.newTodoText} />
```
参数和修饰符
```jsx
<input vOn:click_stop_prevent={this.newTodoText} />
```
v-html
```jsx
<p domPropsInnerHTML={html} />
```
### 函数组件
转译箭头函数函数组件内部返回 JSX ：
```jsx
export default ({ props }) => <p>hello {props.message}</p>
```
或者驼峰形式的函数声明：
```js
const HelloWorld = ({ props }) => <p>hello {props.message}</p>
```
