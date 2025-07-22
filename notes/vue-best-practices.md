# Vue Best Practices Study

- Try to learn something more pn Vue (📝)

## Code related

### Component Design Patterns

#### Please use proper `props` definition with typescript syntax ~

```vue
<script setup>
  interface ExplicitNameOfProps {
    title: string;
    items: Array<{ id: number; name: string}>;
    isLoading?: boolean;
    maxItems?: number;
  }

  const componentNameProps = withDefaults(defineProps<ExplicitNameOfProps>(), {
    title: '',
    items: [],
    isLoading: false,
    maxItems: 10,
  });

  // Or with runtime validation
  const componentNamePropsWithValidation = defineProps({
    title: {
      type: String,
      default: ''
      required: true
    },
    items: {
      type: Array,
      default: () => [],
      validator: (items) => items.every(item => item.id  && item.name)
    },
    isLoading: {
      type: Boolean,
      default: false,
      required: false
    },
    maxItems: {
      type: Number,
      default: 10,
      required: false
    }
  });
</script>
```

#### Implement proper `event` handling (PLEASE DO THIS AS MUCH AS YOU CAN) ~

```vue
<script setup>
import { ref, computed } from 'vue';

interface ComponentNameEmits {
  userUpdated: [user: User];
  userDeleted: [userId: number];
  searchChanged: [term: string];
}

const componentNameEmits = defineEmits<ComponentNameEmits>();
const searchTerm = ref('');
const users = ref<User[]>([]);

const filteredUsers = computed(() => 
  users?.value?.filter(user => user.name.toLowerCase().includes(searchTerm.value.toLowerCase())
));

const handleSearch = () => {
  componentNameEmits('searchChanged', searchTerm.value);
}

const handleEdit = (user: User) => {
  componentNameEmits('userUpdated', user);
}

const handleDelete = (userId: number) => {
  users.value = users.value.filter(user => user.id !== userId);
  componentNameEmits('userDeleted', userId);
}
</script>
```

### State management best practices

#### Use `Pinia` for complex state management ~

```js
import { defineStore } from 'pinia';
import { ref, computed } from 'vue';

export const useUserStore = defineStore('user', () => {
  // States

  // Getters

  // Actions
});
```

## Concept related

<!-- TO BE ADDED -->
