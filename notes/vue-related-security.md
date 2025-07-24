# 🔐 Vue related security considertions

## 🔐 VUE-SPECIFIC SECURITY CHECKLIST FOR FILE DOWNLOADS

### 1. ✅ Always Escape/Encode Dynamic URLs

```html
<!-- ❌ BAD: Unescaped download links from user input -->
<template>
  <a :href="userProvidedUrl">Download</a>
</template>
```

```js
// ✅ GOOD: Sanitize or construct URLs safely
const safeDownloadUrl = `/files/${encodeURIComponent(filename)}`
```

### 2. ✅ Use Blob + URL.createObjectURL Carefully

```ts
const blob = new Blob([data], { type: 'application/pdf' });
const url = URL.createObjectURL(blob);

const link = document.createElement('a');
link.href = url;
link.download = 'safe-file.pdf';
link.click();

URL.revokeObjectURL(url);

// ✅ Ensure data is sanitized
//     - Don't trust input used to generate file content.
//     - Avoid user-controlled MIME types.
```

### 3. ✅ Never Use v-html with Untrusted Download HTML

```html
<!-- ❌ Dangerous if download link is built via innerHTML -->
<div v-html="untrustedHtml"></div>
```

```ts
import DOMPurify from 'dompurify';

const safeHtml = DOMPurify.sanitize(userInputHtml);
```

### 4. ✅ Validate & Whitelist Download File Types

```ts
const ALLOWED_EXTENSIONS = ['pdf', 'csv', 'docx'];
if (!ALLOWED_EXTENSIONS.includes(extension)) {
  throw new Error('Blocked file type');
}
```

### 5. ✅ Use <a download> and Set rel="noopener noreferrer"

```html
<a :href="safeDownloadUrl" download rel="noopener noreferrer">Download</a>
<!-- Prevents tab-nabbing and improves safe file delivery -->
```

### 6. ✅ Don't Use External URLs from User Input Without Validation

```ts
// ❌ Dangerous
window.location.href = userInput;

// ✅ Safer: whitelist hostnames
if (userInput.startsWith('https://trusted.com/files/')) {
  window.location.href = userInput;
}
```

### 7. ✅ Validate Query Params / Route Params for Downloads

```ts
// If we are doing this:
// /download/:filename
router.get('/download/:filename', ...);
// we need to ensure the file name is strictly validated PLeASE
const filename = route.params.filename;
if (!/^[a-zA-Z0-9_-]+\.pdf$/.test(filename)) {
  throw new Error('Invalid filename');
}
```

### 8. ✅ Use refs Over document.querySelector for Downloads

```html
<template>
  <a ref="downloadLink" :href="blobUrl" download="file.pdf">Download</a>
</template>

<script setup lang="ts">
    const downloadLink = ref<HTMLAnchorElement>();

    onMounted(() => {
    downloadLink.value?.click();
    });
</script>
<!-- Why?
    - Vue refs are safer and reactive
    - Avoids brittle DOM queries -->
```


### 9. ✅ Example: Secure Download Button in Vue

```html
<template>
  <button @click="downloadFile">Download Report</button>
</template>

<script setup lang="ts">
    function downloadFile() {
    fetch('/api/report', {
        method: 'GET',
        headers: {
        Authorization: `Bearer ${authToken}`
        }
    })
        .then(res => res.blob())
        .then(blob => {
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = 'report.pdf';
            a.click();
            URL.revokeObjectURL(url);
        })
        .catch(err => console.error('Download failed', err));
    }
</script>
```

## 🔐 TO BE UPDATED ~
