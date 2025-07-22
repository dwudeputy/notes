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
  const users = ref([]);
  const currentUser = ref(null);
  const isLoading = ref(false);
  const error = ref(null);
  // Getters
  const userCount = computed(() => users.value.length);
  const activeUsers = computed(() => users.value.filter(user => user.isActive));
  // Actions
  const fetchUsers = async () => {
    isLoading.value = true;

    try {
      const response = await fetch('/api/users');
      users.value = await response.json();
    } catch (error) {
      error.value = "Fetch users failed ..";
      console.error("Fetch users error: ", error);
    } finally {
      isLoading.value = true;
    }
  }

  const addNewUser = async (userPayload) => {
    try {
      const response = await fetch("/api/users", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringfy(userPayload)
      });
    } catch(error) {
      error.value = "Failed to create a new user ..";
      console.error("Create user error: ", error);
    }
  }

  const setCurrentUser = (user) => {
    currentUser.value = user;
  }

  return {
    // States
    users,
    currentUser,
    isLoading,
    error,
    // Getters
    userCount,
    activeUsers,
    // Actions
    fetchUsers,
    addNewUser,
    setCurrentUser
  }
});
```

## Concept related

<!-- TO BE ADDED -->
