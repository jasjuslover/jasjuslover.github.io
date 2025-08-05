---
layout: post
title: "localhost Jadi Domain Local"
author: jasjuslover
categories: [Opini]
tags: [Opini]
---

Dalam pengembangan aplikasi web modern, caching merupakan teknik penting untuk meningkatkan performa aplikasi dan mengurangi beban server. React Query adalah salah satu library yang banyak digunakan untuk manajemen data dan caching di aplikasi React. Biasanya, React Query menggunakan hook `useQuery` untuk mengambil dan menyimpan data secara otomatis dalam cache. Namun, ada kalanya kita ingin mengelola cache secara manual tanpa menggunakan `useQuery`. Pada artikel ini, kita akan membahas cara menggunakan `queryClient.setQueryData` untuk memanipulasi cache secara langsung.

### Apa itu `queryClient.setQueryData`?

`queryClient.setQueryData` adalah metode yang disediakan oleh React Query untuk memperbarui data cache secara langsung. Dengan menggunakan metode ini, kita dapat menyimpan atau memperbarui data di dalam cache yang dikelola oleh `queryClient` tanpa perlu memicu request API atau menggunakan hook `useQuery`.

Metode ini sangat berguna saat kita perlu mengelola data yang sudah diketahui sebelumnya, atau ketika data berasal dari sumber lain seperti input pengguna atau data yang disimpan secara lokal, dan kita ingin menyinkronkannya dengan cache React Query.

### Langkah-langkah Penggunaan `queryClient.setQueryData`

Berikut adalah langkah-langkah untuk menggunakan `queryClient.setQueryData` secara efektif.

#### 1. Install React Query

Jika Anda belum menginstal React Query di proyek Anda, Anda dapat menambahkannya dengan perintah berikut:

```bash
npm install @tanstack/react-query
```

#### 2. Inisialisasi `queryClient`

Langkah pertama adalah menginisialisasi `queryClient`, yang merupakan objek utama untuk mengelola cache. Biasanya, `queryClient` ini digunakan di dalam komponen root aplikasi Anda.

```javascript
import { QueryClient, QueryClientProvider } from '@tanstack/react-query';

const queryClient = new QueryClient();

function App() {
  return (
    <QueryClientProvider client={queryClient}>
      {/* Aplikasi Anda */}
    </QueryClientProvider>
  );
}
```

#### 3. Menggunakan `queryClient.setQueryData`

`queryClient.setQueryData` digunakan untuk menyimpan atau memperbarui data cache dengan key tertentu. Berikut adalah contoh dasar penggunaannya:

```javascript
import { useQueryClient } from '@tanstack/react-query';

function MyComponent() {
  const queryClient = useQueryClient();

  // Menyimpan data ke dalam cache dengan key 'posts'
  const setCacheData = (newData) => {
    queryClient.setQueryData('posts', newData);
  };

  return (
    <div>
      <button onClick={() => setCacheData([{ id: 1, title: 'New Post' }])}>
        Set Data to Cache
      </button>
    </div>
  );
}
```

Pada contoh di atas, ketika tombol ditekan, data baru diset ke cache dengan key `'posts'`. Anda bisa menggunakan key yang sama saat ingin mengambil data tersebut nanti.

#### 4. Mengambil Data dari Cache

Untuk mengambil data yang disimpan dalam cache, Anda bisa menggunakan `queryClient.getQueryData`:

```javascript
import { useQueryClient } from '@tanstack/react-query';

function MyComponent() {
  const queryClient = useQueryClient();

  // Mengambil data dari cache dengan key 'posts'
  const cacheData = queryClient.getQueryData('posts');

  return (
    <div>
      <h1>Cache Data:</h1>
      <pre>{JSON.stringify(cacheData, null, 2)}</pre>
    </div>
  );
}
```

Di sini, kita mengambil data dari cache dengan key `'posts'` dan menampilkannya di UI.

#### 5. Menggunakan Cache dengan `useMutation`

Biasanya, `useMutation` digunakan untuk melakukan operasi perubahan data, seperti POST, PUT, atau DELETE. Namun, dengan `queryClient.setQueryData`, kita dapat memperbarui cache setelah melakukan perubahan tanpa perlu me-refresh data dengan `useQuery`. Berikut adalah contoh ketika kita mengupdate data cache setelah melakukan operasi mutasi:

```javascript
import { useMutation, useQueryClient } from '@tanstack/react-query';

function MyComponent() {
  const queryClient = useQueryClient();

  const mutation = useMutation({
    mutationFn: (newPost) => fetch('/api/posts', { method: 'POST', body: JSON.stringify(newPost) }),
    onSuccess: (data, variables) => {
      // Setelah mutasi berhasil, perbarui cache dengan data baru
      queryClient.setQueryData('posts', (oldData) => [...oldData, data]);
    },
  });

  const handleAddPost = () => {
    mutation.mutate({ title: 'New Post' });
  };

  return (
    <div>
      <button onClick={handleAddPost}>Add New Post</button>
    </div>
  );
}
```

Dalam contoh ini, setelah mutasi berhasil, kita memperbarui cache `'posts'` dengan data baru yang didapatkan dari server.

### Keuntungan Menggunakan `queryClient.setQueryData`

1. **Manajemen Cache yang Lebih Fleksibel**: Dengan `queryClient.setQueryData`, kita memiliki kontrol lebih atas kapan dan bagaimana data diperbarui dalam cache, tanpa perlu bergantung pada hook `useQuery`.

2. **Optimisasi Performa**: Dengan mengelola cache secara manual, kita dapat meminimalkan panggilan API yang tidak perlu, karena data sudah tersedia dalam cache.

3. **Penggunaan Tanpa Hook**: Terkadang, aplikasi membutuhkan pengelolaan data di luar konteks hook, misalnya di dalam event atau mutasi yang lebih terkontrol.

### Kesimpulan

Menggunakan `queryClient.setQueryData` memberi kita fleksibilitas dalam mengelola data di dalam cache React Query tanpa harus menggunakan `useQuery`. Ini sangat berguna untuk mengoptimalkan aplikasi dengan data yang sering berubah atau berasal dari sumber yang tidak terkait langsung dengan query. Dengan cara ini, kita dapat memperbarui cache secara manual dan menjaga aplikasi tetap responsif tanpa perlu melakukan request ulang ke server.
