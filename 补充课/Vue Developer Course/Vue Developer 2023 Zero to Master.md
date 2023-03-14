## Vue Fundamentals
#### v-model
`v-model`实现双向绑定，和通过事件监听实时修改值的效果相同，（是一种语法糖，更简洁易懂）

## Project 1: Perspective Playground
## Vue: Beyond the Fundamentals
### Understanding Lifecycle Hooks
### Use Lifecycle Hooks
### Virtual DOM
### The Vue Compiler
Vue without the Compiler
Pros:
- 30% lighter than the full version
- 
## Vue Developer Environment
### Overview
### Introduction to Vite
Vite's Pros: 
- Perfomant
- Third Party Lib Support
- Extendable
### Understanding SASS
### PostCSS
SCSS need to be compiled to CSS
PostCSS is a JavaScript lib which can deal with the CSS like Object.
PostCSS is integrated by Vite, so we don't need to install the package.
## Advanced Vue Components
### Sidebar Understanding Server
### Reviewing the Files
### Creating Components
### Styles
### SASS
### Communicating Between Components
Vue provides the way to transfer data between father comp & child comp.
### Props
使用props可以实现父组件向子组件传值，父组件内的数据变化能实时反映到子组件上，反之则不然。
### The Limitations of Porps
### Emitting Events
To produce or trigger an event.
### Validation Props
### Callback Functions
A alternative way to update the data in parent comp from a child comp.
Define the method in parent comp, and transfer this method to child comp through props.
Recommend to use event, cuz every event could be tracked in timeline, but the CB not.
### Inserting Content with Slots

## Transitions & Animations
### Animating with CSS Transition
Vue provides a comp named `transition` to meet the animation need.
*name* prop
use with CSS, the class name shuold be `name-enter-from`, `name-enter-active`, `name-leave-active`, `name-leave-to`. And the CSS prop could be `transition`.
.e.g

### Fine-tuning Transitions
*duration* prop
set the duration time on the HTML comp element.

*mode* prop
Control the transition order. The in and out transition will begin together while this prop  is absent.
- out-in 先出后入，大多数情况下使用此值。
### Animating with CSS Animation
In this case, we use transition comp with `animation` CSS prop.
.e.g

*type* prop
configure the main effect. It could be `transition` / `animation`.

*appear* prop
Show the animation at first render.
### Animating with JS
`transition` also provides events listener.
-   `@before-enter`
-   `@before-leave`
-   `@enter`
-   `@leave`
-   `@appear`
-   `@after-enter`
-   `@after-leave`
-   `@after-appear`
-   `@enter-cancelled`
-   `@leave-cancelled` (`v-show` only)
-   `@appear-cancelled`
### JavaScript Zoom Animation
Web Animation API
We can only use JS to complete animation, add `:css` prop on `<transition>` to skip checking the css code.
## Projects 2: Vue Quiz App
## Master Project: Introduction to Pinia
## Master Project: Form Validation
