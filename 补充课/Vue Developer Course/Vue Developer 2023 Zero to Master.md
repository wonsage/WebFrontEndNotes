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
### Dynamic Components
*is* prop
`<keep-alive>` can keep the comp data in the RAM so that the comp won't be destoried when user change the comp.
## Transitions & Animations
### Animating with CSS Transition
Vue provides a built-in comp named `Transition` to meet the animation need, which can apply enter and leave animations on elements or comps passed to it via its default slot.
`<Transition>` only supports a single element or comp as its slot content.
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
When you add CSS transition and CSS animation at same time, use this prop to configure the main effect. It could be `transition` / `animation`.

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
`HTMLnode.animation(effect, timeline)`
call this in event methods.
*css* prop
We can only use JS to complete animation, add `:css` prop on `<transition>` to skip checking the css code.
### CSS and JavaScript Transition
Using CSS transition or animation, the events also work.
### Animating a List
`<TransitionGroup>`
The diffrence to `<Transition>` is 
### Transition CSS Class Name
There is a popular animation lib: Animate.css. How can we use it with Vue?

*enter-from-class*, *enter-active-class*, *leave-active-class*, *leave-to-class*
To use Animate.css, we only need to change *enter-active-class* and *leave-active-class*
*className* prop
change the class name
## Projects 2: Vue Quiz App
### Setting up
Initiate a new proj with Vite and trim it up.
### Rendering the Questions
data drive view
When show the finish tip?
Which question is showing?

### Moving between Questions
Pass data through prop
1. Loop through all questions and render them
2. Keep track of current active question and only display that question.
   `v-if`
3. Listen for click events on answer.  
   `@click`, `$emit`
4. Check if answer is correct, if answer is correct, keep track of how many answers are correct.  Update number of questions answered.
   `++`, `if`
5. Update current active question to the next question.
### Finishing Touches
## Master Project: Introduction to Pinia
We are focusing at the core of Vue in the preview courses. The next to come is a full project, including router, states, and style orgnazition.
### Creating a New Project
Config a new Vue proj with Router, Pinia, Vitest, ESLint, Prettier.
### Reviewing the Files
at root directory
- *.eslintrc.cjs*
- *.prettierrc.json*
- *cypress.config.js*
- *package.json*
### Formatting with ESLint and Prettier
### What is Tailwind
- Does not come with UI elements
- Focuses on utility

PurgeCSS
### 007. Installing Tailwind
### 009. Loading Assets
assets files, will be processed by Vite => `./src/assets`
static files, like postCSS or => `./public`
### 010. Understanding State
**State** refers to the data for app.
In the simple app, data is passed by prop from comp to child comp.
State manager solution is a single location where all your data is stored and managed, and you can access it globally.
**Pinia**
### 011. Reviewing the Pinia Config
### 12. Splitting the Template into Comp
### 13. Disabling Vue's Rules
`.eslintrc.cjs` => `rules`
### 14. Working with State
1. new create a store.  
   `@/stores` new build a .js file
   config the store, like id, state(data), getter(methods)...
   
2. Use store in comp.  
   import **use*Id*Store**, and also **mapStores** if you are using options API
### 15. Alternative Mapping Functions
- mapState
- mapWritableState
These two functions are both generate a object
The difference is that `mapWriteableState` can't add store's getter.
### Understanding Getters
### 17. Using Getters
Define a getter for class name in Store, it returns different class name in different state cases.
Register the Store in Comp (using **mapState**), and access the classname Getter via Computed.
Apply the classname to element, so that the element can change with State in Store.
### 18. Closing the Modal
Register the Store in Comp (using **mapWritableState**)
write the State's value.
### 19. Aliases
Rename the state in comp
Use object instead of array param, like
`mapState(useUserStore, ['name', 'age'])` => `mapState(useUserStore, {userName: 'name', userAge: 'age'}`
### 20. Adding Tabs
Define a var to record current tab. When user click on tab, var change its val.
Tab button's style and tab comp's visibility will come along with the var.
## Master Project: Form Validation
### 03. Validation Component
1. Use the `<field />` component
2. Assign a name to the input
3. Add the rules
4. Handle the errors
### Defining Rules
install rule pkg
### Appling Rules
#### Filed-level Validation
`rule` prop on vee-field 
#### Form-level Validation
`:validation-schema="simpleSchema"` add to `<vee-form>`
Schema Object is like:
```
simpleSchema: {
	email: 'required',
	name: 'required',
}
```
Schema's advantage is we can centralize all the rules in a obj.
**Yup** is a validator bundle matchs VeeValidate, it's helpful to apply different rules to fields easily.
```
simpleSchema: {
	email: yup.string().required().email(),
	name: yup.string().reueired(),
}
```
**@vee-validate/rules** is another rules pkg for vv
Use the `defineRule` function to add a rule exported by thie lib to global rules.
When should the error message appear? If the field is touched.
`<ErrorMessage>` is available, add `name` prop matches the `field`'s name.
### Additional Rules
There are many rules in the pkg, refer to this [link](https://vee-validate.logaretm.com/v4/guide/global-validators#available-rules)
### Validating Email
*email* rule
### Validating Numer
*min_value* & *max_value* rule
### Validating Passwords
*confirm_password* rule
`confirm_password: 'confirm_password:@password'`
### 10. Downdrop and Checkbox Field
### 11. Validating the Form
add `@submit` event method on the `vee-form`, only if all input validation pass, the function  will get the form object as params.
### 12. Sidebar Slot Property
### 13. Rendering Multiple Error Messages
In some cases, you may want to output multiple errors for a specific input, for example password input.
[like](https://vee-validate.logaretm.com/v3/guide/basics.html#multiple-messages)
*bails* prop of `vee-form`
default: True, fast exit, it's a strategy to make sure the faster feedback and fewer resources. If the first input valid, then neither the second one.
set it to False, run all the rules
*bails* is also an option of `configure` function, which can turn off fast exit globally.
### 14. Default Values
*initial-values* prop of `vee-form`
### 15. Custom Error Messages
Custom tips by override the validate function's return value from False to String.
We can config a function API `generateMessage`, and then if the validate function pass failed, False will be replaced by custom message from `generateMessage`.
[Configuration (logaretm.com)](https://vee-validate.logaretm.com/v4/api/configuration#config-options)
1. Import `configure` function from pkg
2. Config the validation by calling `configure` with options object.
3.  `generateMessage` is one of options, 
### 16. Validation Triggers
- *validateOnChange*: After the change event
- *validateOnBlur*: After the blur event
- If the v-model directive is applied to an input, after the 
- form submit
### 17. 
### 18. Setting up the Login Form
## Authentication
### 01. Understanding Authentication
Introducing Firebase, a back-end is suitable for proto and demo.
### 05. Handling the Response
Firebase handles the user registeration, email is the primary key.
### 07. Store the data
3 of firebase:
Collection
Document
### 09. Understanding the Authentication
Firebase is a server software deployed on remote server.
Change the rules of firebase to make sure data is only writable for user logged in.
### 10. 
### 11. Understanding Actions
Pinia is different with VueX

### 12. Using Actions
`mapActions()`
### 13. Connecting 
In the before lectures, we use `firebase.firestore().collection('Users').add({})` to add a `document` in the *User* Collection.
`add` function is belong to *CollectionReference*, means we were manual at collection level.

In this lecture, we want to keep the uid of data in firestore same with uid of data in Auth Database.
So we use `firebase.firestore().collection('Users').doc()`
[doc func](https://firebase.google.com/docs/reference/js/v8/firebase.firestore.CollectionReference?authuser=0#doc) is belong to *CollectionReference*, and return *DocumentReference*. It's param
`set` function is belong to *DocumentReference*, 
### 14.Initializing Firebase First
[onAuthStateChanged](https://firebase.google.com/docs/reference/js/v8/firebase.auth.Auth?authuser=0#onauthstatechanged)
This func's param is a observer callback, which will be triggered on sign-in or sign-out.
### 15. Persisting the User Authentication
In `APP` root comp, the 1st init comp.
Use `auth.currentUser` to judge whether logged In or not. This API is provided by firebase SDK, the prog search user's token in localStorage which should be stored on logged-in.
### 16. Setting up the Login
`auth.signOut()`
### 17. 
### 18. Sidebar
jwt: JSON Web Token
SSL certicification is important and necessary.
## Route
### 01. Understanding Routing
### Reviewing the Router Configuration
### Creating Routes
1. configure Router `@/route/index.js`
2. Replace the main content of root comp with `<router-view>`
### History Mode
History Mode: 
### 05. Navigating with Link
1. Replace the link element `<a>` with `<router-link>`
2. Config the prop *to* :
	1. with `/` : absolute address
	2. without `/` : relatvie address, only change the lowest level link.  
### Custom Links

### Tailwind Styles for Active Links
### Naming Routes
Use name obj as prop *to*'s value instead of path.

### Setting up “Catch-All” and Redirect Routes

### Route Alias

### Guarding Routes
    - golbal Guard
    - 

### Route Specific Guards
    
    04:54
    
### Guarding Authentication Only Routes

### Redirecting after Logging Out

-   Route Meta Fields
  
## Uploading  Files
### 01. Preparing the Upload Component

### 02. Handling Drag and Drop Events
drag event

### Handling the File

### Enabling Firebase’s Storage Service

### Uploading Files with Firebase
[Storage.ref | JavaScript SDK  |  Firebase JavaScript API reference (google.com)](https://firebase.google.com/docs/reference/js/v8/firebase.storage.Storage#ref)

[Reference.child() | JavaScript SDK  |  Firebase JavaScript API reference (google.com)](https://firebase.google.com/docs/reference/js/v8/firebase.storage.Reference#child)
[Reference.put() | JavaScript SDK  |  Firebase JavaScript API reference (google.com)](https://firebase.google.com/docs/reference/js/v8/firebase.storage.Reference#put)

### Firebase Rules and Validation

### Adding the Progress Bar
[UploadTask | JavaScript SDK  |  Firebase JavaScript API reference (google.com)](https://firebase.google.com/docs/reference/js/v8/firebase.storage.UploadTask)
[UploadTask.on](https://firebase.google.com/docs/reference/js/v8/firebase.storage.UploadTask#on)
UploadTask.snapshot  => [UploadTaskSnapshot | JavaScript SDK  |  Firebase JavaScript API reference (google.com)](https://firebase.google.com/docs/reference/js/v8/firebase.storage.UploadTaskSnapshot)
UploadTaskSnapshot.ref => [Reference | JavaScript SDK  |  Firebase JavaScript API reference (google.com)](https://firebase.google.com/docs/reference/js/v8/firebase.storage.Reference)
### Making the Progress Bar Dynamic

###  Improving the Progress Bar

### Handling Errors and Successful Uploads

### 11.Storing the File Data in the Database
We have stored the audio file in the *Storage*, but we cant know who uploaded the file. So we need storing some additional infomations after the file upload request success, includes uid, file name, etc.
File name is expanded to original name and modified name. During uploading process, these two names are initialized as same as file name. While user can change the modified name after uploading.
Using [Reference.getDownloadURL() | JavaScript SDK  |  Firebase JavaScript API reference (google.com)](https://firebase.google.com/docs/reference/js/v8/firebase.storage.Reference#getdownloadurl) to fetch a long lived download URL for the song uploaded.
### 12. Firebase References and Snapshots
the differences between references and snapshots:
References and sanpshots can read the data in the application. Snapshots are read-only but are memory efficient.
### 13.  Fallback Upload
Add `input` element to upload files
### 14. Canceling Uploads
Stop request when the comp is unmounted.
[UploadTask.cancel](https://firebase.google.com/docs/reference/js/v8/firebase.storage.UploadTask#cancel)
- Method 1: call the `cancel` func on comp's `beforeUnmount`

### Canceling Uploads with Ref
- Method 2:  call the `cancel` func at parent comp's `beforeRouteLeave`

This way need using `$ref` API.
### 16. One more thing about References
We can also select the native HTML DOM object with `ref`, and change its content. But cannot modify its Vue Instance's data.

**Reactivity**
References

###  17. Querying the Database
We've finished the upload part, the other half part is getting the songs user uploaded.
### 18.Storing the List of Songs
We use [CollectionReference.where() | JavaScript SDK  |  Firebase JavaScript API reference (google.com)](https://firebase.google.com/docs/reference/js/v8/firebase.firestore.CollectionReference#where) function to get the *Documents* we need in *Collection*.

### 19.Displaying the List of Songs
Seperate `CompositionItem` comp out for each single song
### 20.Prop Validation
Pass the song info obj to each `CompositionItem` comp through `song` prop.
### 21.Toggling the Form
Toggle the edit form by clicking pen-icon.
### 22.Validating the Song Form 
Using *Vee-Validation* to validate the edit form.
### 23. Editing a Song

### 24. Deleting a Song from the Storage/Database

### 25.Updating the list of songs after an Upload
### 26. Router Leave Guards

## Playing Music
### 01. Creating the Home Page
###  02. Checking the Scroll Position
### 03. Infinite Scrolling
To know when page reach bottom.
### 04. Path Parameters
route params

### 05. Creating the Song Template
### 06. Validating the Comment
    
    03:58
    
-   Prepping the Form
    
    04:42
    
-   Finalizing the Comment Form
    
    10:23
    
### 09. Displaying the Comments
We need to get comments at two times:
- load *song* page.
- after commit a comment.
### 10. Updating the Comments List

### 11. Query Parameters
Query data from database with parameters.
Router supports query params, they will show in the url, so we can get the sort way directly.
Add watcher for *sort*.
### 12.Detecting Query Parameters
Using `$route.query` to get query params.
- **Path Parameters** should be used for returning a single resource or multiple resources.
- **Query Parameters** should be used for sorting/filtering through data.
### 13. Updating the Comment Count
1. local data comment count +1
2. databse comment count +1
   ##
### 14.Storing the song in the State

### 15.Playing Audio
Using *Howler* lib in *Store Action* to play audio.
### 16.Toggling Audio

### 17.Duration and Current Position
### 18.Formatting the Time

 Player Progress Bar
    
    08:21
    
-   Changing the Audio Position
    
    10:23
    
-   Extra Exercise: Update the "play" Button
    
    00:22
    
-   Creating links with Hash Fragments
    
    04:48
    
-   Route Transitions
## Directives
### 01.Introduction to Directives
    
    05:31
    
-   Writing our First Directive
    
    05:47
    
-   Passing Values to Directives
    
    05:22
    
-   Directive Modifiers
    
    05:06
    
-   Registering a Directive Locally