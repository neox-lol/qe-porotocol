<template>
  <div class="">
    <ul role="list" class="mx-auto mt-20 max-w-2xl grid gap-x-8 gap-y-14 grid-cols-1 sm:grid-cols-2 lg:max-w-none lg:mx-0 lg:grid-cols-3 xl:grid-cols-4">
      <li v-for="person in people" :key="person.name">
        <img class="object-cover rounded-2xl w-full aspect-[14/13]" :src="person.imageUrl" alt="" />
        <h3 class="font-semibold mt-6 text-lg text-white tracking-tight leading-8">{{ person.name }}</h3>
        <p class="text-base text-gray-300 leading-7">{{ person.role }}</p>
        <p class="text-sm text-gray-500 leading-6">{{ person.location }}</p>
      </li>
    </ul>
  </div>
</template>

<script setup>
const people = [
  {
    name: 'Leslie Alexander',
    role: 'Co-Founder / CEO',
    imageUrl:
      'https://images.unsplash.com/photo-1494790108377-be9c29b29330?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=8&w=1024&h=1024&q=80',
    location: 'Toronto, Canada',
  },
  {
    name: 'Leslie Alexander',
    role: 'Co-Founder / CEO',
    imageUrl:
      'https://images.unsplash.com/photo-1494790108377-be9c29b29330?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=8&w=1024&h=1024&q=80',
    location: 'Toronto, Canada',
  },
  {
    name: 'Leslie Alexander',
    role: 'Co-Founder / CEO',
    imageUrl:
      'https://images.unsplash.com/photo-1494790108377-be9c29b29330?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=8&w=1024&h=1024&q=80',
    location: 'Toronto, Canada',
  },
  {
    name: 'Leslie Alexander',
    role: 'Co-Founder / CEO',
    imageUrl:
      'https://images.unsplash.com/photo-1494790108377-be9c29b29330?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=8&w=1024&h=1024&q=80',
    location: 'Toronto, Canada',
  },
]
</script>