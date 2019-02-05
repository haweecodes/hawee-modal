# hawee-modal

## Install
```
npm i hawee-modal
```

### How to use
Include module to the file you want to use it in
```
import Modal from 'hawee-modal'
import 'hawee-modal/dist/h-modal.css'
```
Create modal
```vue
<Modal v-model="isVisible">
  hello, world!
</Modal>
```

####Declare Size
There are three types of size available
- small (by default)
- medium
- large

example is given below
```vue
<Modal v-model="isVisible" size="large">
  hello, world!
</Modal>
```

####Declare Type
There are three types of size available
- info (by default)
- error
- warning

example is given below
```vue
<Modal v-model="isVisible" type="error">
  hello, world!
</Modal>
```