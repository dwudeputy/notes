# Vue Demo (Examples) - Vue Study


## Examples


### Example 1: Attribute bindings ~

```html
<script setup>
  import { ref } from 'vue';

  const message = ref('Hellow World!');
  const isRed = ref(true);
  const color = ref('green');

  function toggleRed() {
    isRed.value = !isRed.value
  }

  function toggleColor() {
    color.value = color.value === 'green' ? 'blue' : 'green';
  }
</script>
<template>
  <p :class="{ red: idRed }" @click="toggleRed">This is Red color toggle text ~</p>
  <p :style="{ color }" @click="toggleColor">Text color toggle between blue and green ~</p>
</template>
<style>
  .red {
    color: red;
  }
</style>
```


### Example 2: Form bindings ~

```html
<script setup>
  import { ref } from 'vue';

  const text = ref('Edit me');
  const checked = ref(true);
  const checkedNames = ref(['Jack']);
  const picked = ref('One');
  const selected = ref(['A']);
</script>

<template>
  <h2>Text Input</h2>
  <input v-model="text" />
  <p>{{ text }}</p>

  <h2>Checkbox</h2>
  <input type="checkbox" id="checkbox" v-model="checked" />
  <label for="checkbox">Checked: {{ checked }}</label>

  <h2>Multi-Checkbox</h2>
  <input type="chekbox" id="jack" value="Jack" v-model="checkedNames" />
  <label for="jack">Jack</label>
  <input type="chekbox" id="john" value="John" v-model="checkedNames" />
  <label for="john">John</label>
  <input type="chekbox" id="mike" value="Mike" v-model="checkedNames" />
  <label for="mike">Mike</label>
  <p>Checked names: {{ checkedNames }}</p>

  <h2>Radio</h2>
  <input type="radio" id="one" value="One" v-model="picked" />
  <label for="one">One</label>
  <br />
  <input type="radio" id="two" value="Two" v-model="picked" />
  <label for="two">Two</label>
  <p>{{ picked }}</p>

  <h2>Select</h2>
  <select v-model="selected">
    <option disabled value="">Please select one</option>
    <option>A</option>
    <option>B</option>
    <option>C</option>
  </select>
  <p>{{ selected }}</p>

  <h2>Multi-Select</h2>
  <select v-model="multiSelected" multiple style="width:100px">
    <option>A</option>
    <option>B</option>
    <option>C</option>
  </select>
  <p>Selected: {{ multiSelected }}</p>
</template>
```

### Example 3: Modal with Transitions ~

```html
<!-- // App.Vue -->
<script setup>
  import Modal from './Modal.vue';
  import { ref } from 'vue';

  const showModal = ref(false);
</script>
<template>
  <button id="show-modal" @click="showModal = true">Show Modal</button>
  <Teleport to="body">
    <modal :show="showModal" @close="showModal = false">
      <template>
        <h3>Customer Header</h3>
      </template>
    </modal>
  </Teleport>
</template>
```

```html
<!-- // Modal.vue -->
<script setup>
  const props = defineProps({
    show: Boolean
  });
</script>
<template>
  <Transition>
    <div v-if="show" class="modal-mask">
      <div class="modal-container">
        <div class="modal-header">
          <slot name="header">default header</slot>
        </div>
        <div class="modal-body">
          <slot name="body">default body</slot>
        </div>
        <div class="modal-footer">
          <slot name="footer">
            default footer
            <button class="modal-default-button" @click="$emit('close')">OK</button>
          </slot>
        </div>
      </div>
    </div>
  </Transition>
</template>
<style scoped>
  .modal-mask {
    position: fixed;
    z-index: 9998;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    transition: opacity 0.3s ease;
  }

  .modal-container {
    width: 300px;
    margin: auto;
    padding: 20px 30px;
    background-color: #fff;
    border-radius: 2px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
    transition: all 0.3s ease;
  }

  .modal-header h3 {
    margin-top: 0;
    color: #42b983;
  }

  .modal-body {
    margin: 20px 0;
  }

  .modal-default-button {
    float: right;
  }

  /*
  * The following styles are auto-applied to elements with
  * transition="modal" when their visibility is toggled
  * by Vue.js.
  *
  * You can easily play with the modal transition by editing
  * these styles.
  */

  .modal-enter-from {
    opacity: 0;
  }

  .modal-leave-to {
    opacity: 0;
  }

  .modal-enter-from .modal-container,
  .modal-leave-to .modal-container {
    -webkit-transform: scale(1.1);
    transform: scale(1.1);
  }
</style>
```

### Example 4: List with Transitions ~

```html
<script setup>
  import { shuffle as _shuffle } from 'lodash-es';
  import { ref } from 'vue';

  const getInitialItems = () => [1, 2, 3, 4, 5];
  const items = ref(getInitialItems());
  let id = items.value.length + 1;

  function insert() {
    const i = Math.round(Math.random() * items.value.length);
    items.value.splice(i, 0, id++);
  }

  function reset() {
    items.value = getInitialItems();
    id = items.value.length + 1;
  }

  function shuffle() {
    items.value = _shuffle(items.value);
  }

  function remove(item) {
    const i = items.value.indexOf(item);

    if(i > -1) {
      items.value.splice(i, 1);
    }
  }
</script>
<template>
  <button @click="insert">Insert at random index</button>
  <button @click="reset">Reset</button>
  <button @click="shuffle">Shuffle</button>
  <TransitionGroup tag="ul" name="fade" class="container">
    <li v-for="item in items" class="item" :key="item">
      {{ item }}
      <button @click="remove(item)">X</button>
    </li>
  </TransitionGroup>
</template>
<style scoped>
  .container {
    position: relative;
    padding: 0;
    list-style-type: none;
  }

  .item {
    width: 100%;
    height: 30px;
    background-color: #f3f3f3;
    border: 1px solid #666;
    box-sizing: border-box;
  }

  /* 1. declare transition */
  .fade-move,
  .fade-enter-active,
  .fade-leave-active {
    transition: all 0.5s cubic-bezier(0.55, 0, 0.1, 1);
  }

  /* 2. declare enter from and leave to state */
  .fade-enter-from,
  .fade-leave-to {
    opacity: 0;
    transform: scaleY(0.01) translate(30px, 0);
  }

  /* 3. ensure leaving items are taken out of layout flow so that moving
        animations can be calculated correctly. */
  .fade-leave-active {
    position: absolute;
  }
</style>
```