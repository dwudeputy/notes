# Vue Component Testing Best Practices (Keep updating)

## 🚫 **Bad Practices to Avoid**

### 1. **Accessing Internal State via `wrapper.vm`**

❌ **Bad:**
```javascript
// Directly manipulating internal state
wrapper.vm.state.loading = false;
wrapper.vm.state.userAlreadyOnboarded = true;
expect(wrapper.vm.page).toBe(2);
```

✅ **Good:**
```javascript
// Test through props and external behavior
await wrapper.setProps({ loading: false, userAlreadyOnboarded: true });
expect(wrapper.findComponent(PaginationComponent).props('currentPage')).toBe(2);
```

### 2. **Calling Internal Methods Directly**

❌ **Bad:**
```javascript
// Calling private methods
wrapper.vm.manageLink();
wrapper.vm.handleSubmit();
```

✅ **Good:**
```javascript
// Test through user interactions
await wrapper.find('[data-testid="manage-button"]').trigger('click');
await wrapper.find('[data-testid="submit-form"]').trigger('submit');
```

### 3. **Testing Implementation Details**

❌ **Bad:**
```javascript
// Testing internal state changes
expect(wrapper.vm.internalCounter).toBe(5);
expect(wrapper.vm.state.isProcessing).toBe(true);
```

✅ **Good:**
```javascript
// Testing visible behavior and outputs
expect(wrapper.find('[data-testid="counter"]').text()).toBe('5');
expect(wrapper.find('[data-testid="loading-spinner"]').exists()).toBe(true);
```

## ✅ **Best Practices**

### 1. **Test User Interactions**
```javascript
// Simulate real user behavior
await wrapper.find('[data-testid="email-input"]').setValue('test@example.com');
await wrapper.find('[data-testid="submit-button"]').trigger('click');
```

### 2. **Use Props for State Testing**
```javascript
// Pass state through props instead of manipulating internal state
const wrapper = mount(Component, {
  props: {
    loading: true,
    userAlreadyOnboarded: '123',
    disabled: false
  }
});
```

### 3. **Test Emitted Events**
```javascript
// Test component communication
await wrapper.find('[data-testid="close-button"]').trigger('click');
expect(wrapper.emitted('close')).toBeTruthy();
expect(wrapper.emitted('close')[0]).toEqual(['reason']);
```

### 4. **Mock External Dependencies**
```javascript
// Mock API calls and external services
vi.mock('@/api/service', () => ({
  fetchUserData: vi.fn().mockResolvedValue({ id: '123', name: 'John' })
}));
```

### 5. **Test Component Props and Attributes**
```javascript
// Test component communication through props
expect(wrapper.findComponent(ChildComponent).props('userId')).toBe('123');
expect(wrapper.find('[data-testid="input"]').attributes('disabled')).toBeDefined();
```

### 6. **Use Data Test IDs**
```javascript
// Use data-testid for reliable element selection
expect(wrapper.find('[data-testid="user-profile"]').exists()).toBe(true);
expect(wrapper.find('[data-testid="error-message"]').text()).toContain('Invalid email');
```

### 7. **use `flushPromises`**

```javascript
// ❌ BAD: Direct state manipulation
wrapper.vm.state.loading = false;
// ✅ GOOD: Wait for natural async completion
await flushPromises();
```

## 🔧 **Refactoring Examples**

### Example 1: Pagination Testing

**Before:**
```javascript
wrapper.findComponent(PaginationComponent).vm.$emit('next');
expect(wrapper.vm.page).toBe(2);
```

**After:**
```javascript
await wrapper.findComponent(PaginationComponent).vm.$emit('next');
expect(wrapper.findComponent(PaginationComponent).props('currentPage')).toBe(2);
```

### Example 2: State-Dependent Rendering

**Before:**
```javascript
wrapper.vm.state.userAlreadyOnboarded = true;
await nextTick();
expect(wrapper.findComponent(WaLink).exists()).toBe(true);
```

**After:**
```javascript
const wrapper = mount(Component, {
  props: { userAlreadyOnboarded: true }
});
expect(wrapper.findComponent(WaLink).exists()).toBe(true);
```

### Example 3: Navigation Testing

**Before:**
```javascript
await link.trigger('click');
expect(mockPush).toHaveBeenCalledWith(`#team/${wrapper.vm.state.userAlreadyOnboarded}/hr`);
```

**After:**
```javascript
const employeeId = '1';
const wrapper = mount(Component, {
  props: { userAlreadyOnboarded: employeeId }
});
await link.trigger('click');
expect(mockPush).toHaveBeenCalledWith(`#team/${employeeId}/hr`);
```

## 🎯 **Key Principles**

1. **Test behavior, not implementation**
2. **Test from the user's perspective**
3. **Use props and events for component communication**
4. **Mock external dependencies, not internal state**
5. **Make tests resilient to refactoring**
6. **Use descriptive test names and data-testid attributes**

## 🚀 **Benefits of Good Testing Practices**

- **Maintainable**: Tests don't break when internal implementation changes
- **Reliable**: Tests reflect real user behavior
- **Readable**: Tests clearly show what the component should do
- **Fast**: Tests run quickly without complex setup
- **Confident**: Tests give confidence that the component works as expected

---

*Remember: If you need to access `wrapper.vm` to test something, consider whether that thing should be exposed through props, events, or visible behavior instead.*
