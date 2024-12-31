<template>
  <div class="mx-auto mt-28 max-w-7xl px-6 sm:mt-56 lg:px-8">
    <div class="opacity-30 transform-gpu inset-x-0 top-1/2 -z-10 -translate-y-1/2 absolute overflow-hidden blur-3xl" aria-hidden="true">
      <div class="bg-gradient-to-tr from-[#ff80b5] to-[#9089fc] ml-[max(50%,38rem)] w-[82.0625rem] aspect-[1313/771]" style="clip-path: polygon(74.1% 44.1%, 100% 61.6%, 97.5% 26.9%, 85.5% 0.1%, 80.7% 2%, 72.5% 32.5%, 60.2% 62.4%, 52.4% 68.1%, 47.5% 58.3%, 45.2% 34.5%, 27.5% 76.7%, 0.1% 64.9%, 17.9% 100%, 27.6% 76.8%, 76.1% 97.7%, 74.1% 44.1%)" />
    </div>
    <div class="flex opacity-25 transform-gpu pt-32 inset-x-0 top-0 -z-10 absolute overflow-hidden blur-3xl sm:pt-40 xl:justify-end" aria-hidden="true">
      <div class="bg-gradient-to-tr flex-none from-[#ff80b5] to-[#9089fc] ml-[-22rem] origin-top-right w-[82.0625rem] rotate-[30deg] aspect-[1313/771] xl:mr-[calc(50%-12rem)] xl:ml-0" style="clip-path: polygon(74.1% 44.1%, 100% 61.6%, 97.5% 26.9%, 85.5% 0.1%, 80.7% 2%, 72.5% 32.5%, 60.2% 62.4%, 52.4% 68.1%, 47.5% 58.3%, 45.2% 34.5%, 27.5% 76.7%, 0.1% 64.9%, 17.9% 100%, 27.6% 76.8%, 76.1% 97.7%, 74.1% 44.1%)" />
    </div>
    <div class="mx-auto max-w-7xl px-6 lg:px-8">
      <div class="mx-auto max-w-xl text-center" v-motion-slide-visible-right>
        <h2 class="font-semibold text-lg tracking-tight text-lime-600 leading-8">Testimonials</h2>
        <p class="font-bold mt-2 tracking-tight text-3xl text-gray-300 sm:text-4xl">Loved by crypto native people.</p>
      </div>
      <div v-motion-slide-visible-top class="mx-auto mt-16 text-sm max-w-2xl grid text-gray-900 leading-6 gap-8 grid-cols-1 grid-rows-1 sm:mt-20 sm:grid-cols-2 xl:max-w-none xl:mx-0 xl:grid-flow-col xl:grid-cols-4">
        <figure class="bg-white rounded-2xl shadow-lg ring-1 ring-gray-900/5 sm:col-span-2 xl:col-start-2 xl:row-end-1">
          <blockquote class="font-semibold text-lg tracking-tight p-6 text-gray-900 leading-7 sm:text-xl sm:p-12 sm:leading-8">
            <p>{{ `“${featuredTestimonial.body}”` }}</p>
          </blockquote>
          <figcaption class="border-t flex flex-wrap border-gray-900/10 py-4 px-6 gap-x-4 gap-y-4 items-center sm:flex-nowrap">
            <img class="rounded-full flex-none bg-gray-50 h-10 w-10" :src="featuredTestimonial.author.imageUrl" alt="" />
            <div class="flex-auto">
              <div class="font-semibold">{{ featuredTestimonial.author.name }}</div>
              <div class="text-gray-600">{{ `@${featuredTestimonial.author.handle}` }}</div>
            </div>
            <img class="flex-none h-10 w-auto" :src="featuredTestimonial.author.logoUrl" alt="" />
          </figcaption>
        </figure>
        <div v-for="(columnGroup, columnGroupIdx) in testimonials" :key="columnGroupIdx" class="space-y-8 xl:space-y-0 xl:contents">
          <div v-for="(column, columnIdx) in columnGroup" :key="columnIdx" :class="[(columnGroupIdx === 0 && columnIdx === 0) || (columnGroupIdx === testimonials.length - 1 && columnIdx === columnGroup.length - 1) ? 'xl:row-span-2' : 'xl:row-start-1', 'space-y-8']">
            <template v-if="columnGroupIdx === 0">
              <figure v-motion-slide-visible-left v-for="testimonial in column" :key="testimonial.author.handle" class="bg-white rounded-2xl shadow-lg p-6 ring-1 ring-gray-900/5">
                <blockquote class="text-gray-900">
                  <p>{{ `“${testimonial.body}”` }}</p>
                </blockquote>
                <figcaption class="flex mt-6 gap-x-4 items-center">
                  <img class="rounded-full bg-gray-50 h-10 w-10" :src="testimonial.author.imageUrl" alt="" />
                  <div>
                    <div class="font-semibold">{{ testimonial.author.name }}</div>
                    <div class="text-gray-600">{{ `@${testimonial.author.handle}` }}</div>
                  </div>
                </figcaption>
              </figure>
            </template>
            <template v-if="columnGroupIdx === 1">
              <figure v-motion-slide-visible-right v-for="testimonial in column" :key="testimonial.author.handle" class="bg-white rounded-2xl shadow-lg p-6 ring-1 ring-gray-900/5">
                <blockquote class="text-gray-900">
                  <p>{{ `“${testimonial.body}”` }}</p>
                </blockquote>
                <figcaption class="flex mt-6 gap-x-4 items-center">
                  <img class="rounded-full bg-gray-50 h-10 w-10" :src="testimonial.author.imageUrl" alt="" />
                  <div>
                    <div class="font-semibold">{{ testimonial.author.name }}</div>
                    <div class="text-gray-600">{{ `@${testimonial.author.handle}` }}</div>
                  </div>
                </figcaption>
              </figure>
            </template>

          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const featuredTestimonial = {
  body: 'Integer id nunc sit semper purus. Bibendum at lacus ut arcu blandit montes vitae auctor libero. Hac condimentum dignissim nibh vulputate ut nunc. Amet nibh orci mi venenatis blandit vel et proin. Non hendrerit in vel ac diam.',
  author: {
    name: 'Brenna Goyette',
    handle: 'brennagoyette',
    imageUrl:
      'https://images.unsplash.com/photo-1550525811-e5869dd03032?ixlib=rb-=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=1024&h=1024&q=80',
    logoUrl: 'https://tailwindui.com/img/logos/savvycal-logo-gray-900.svg',
  },
}
const testimonials = [
  [
    [
      {
        body: 'Laborum quis quam. Dolorum et ut quod quia. Voluptas numquam delectus nihil. Aut enim doloremque et ipsam.',
        author: {
          name: 'Leslie Alexander1',
          handle: 'lesliealexander',
          imageUrl:
            'https://images.unsplash.com/photo-1494790108377-be9c29b29330?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
        },
      },
      {
        body: 'Laborum quis quam. Dolorum et ut quod quia. Voluptas numquam delectus nihil. Aut enim doloremque et ipsam.',
        author: {
          name: 'Leslie Alexander2',
          handle: 'lesliealexander',
          imageUrl:
            'https://images.unsplash.com/photo-1494790108377-be9c29b29330?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
        },
      },
      {
        body: 'Laborum quis quam. Dolorum et ut quod quia. Voluptas numquam delectus nihil. Aut enim doloremque et ipsam.',
        author: {
          name: 'Leslie Alexander3',
          handle: 'lesliealexander',
          imageUrl:
            'https://images.unsplash.com/photo-1494790108377-be9c29b29330?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
        },
      },
      {
        body: 'Laborum quis quam. Dolorum et ut quod quia. Voluptas numquam delectus nihil. Aut enim doloremque et ipsam.',
        author: {
          name: 'Leslie Alexander4',
          handle: 'lesliealexander',
          imageUrl:
            'https://images.unsplash.com/photo-1494790108377-be9c29b29330?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
        },
      },
      // More testimonials...
    ],
    [
      {
        body: 'Aut reprehenderit voluptatem eum asperiores beatae id. Iure molestiae ipsam ut officia rem nulla blanditiis.',
        author: {
          name: 'Lindsay Walton5',
          handle: 'lindsaywalton',
          imageUrl:
            'https://images.unsplash.com/photo-1517841905240-472988babdf9?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
        },
      },
      {
        body: 'Aut reprehenderit voluptatem eum asperiores beatae id. Iure molestiae ipsam ut officia rem nulla blanditiis.',
        author: {
          name: 'Lindsay Walton6',
          handle: 'lindsaywalton',
          imageUrl:
            'https://images.unsplash.com/photo-1517841905240-472988babdf9?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
        },
      },
      // More testimonials...
    ],
  ],
  [
    [
      {
        body: 'Voluptas quos itaque ipsam in voluptatem est. Iste eos blanditiis repudiandae. Earum deserunt enim molestiae ipsum perferendis recusandae saepe corrupti.',
        author: {
          name: 'Tom Cook7',
          handle: 'tomcook',
          imageUrl:
            'https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
        },
      },
      {
        body: 'Voluptas quos itaque ipsam in voluptatem est. Iste eos blanditiis repudiandae. Earum deserunt enim molestiae ipsum perferendis recusandae saepe corrupti.',
        author: {
          name: 'Tom Cook8',
          handle: 'tomcook',
          imageUrl:
            'https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
        },
      },
      // More testimonials...
    ],
    [
      {
        body: 'Molestias ea earum quos nostrum doloremque sed. Quaerat quasi aut velit incidunt excepturi rerum voluptatem minus harum.',
        author: {
          name: 'Leonard Krasner9',
          handle: 'leonardkrasner',
          imageUrl:
            'https://images.unsplash.com/photo-1519345182560-3f2917c472ef?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
        },
      },
      {
        body: 'Molestias ea earum quos nostrum doloremque sed. Quaerat quasi aut velit incidunt excepturi rerum voluptatem minus harum.',
        author: {
          name: 'Leonard Krasner',
          handle: 'leonardkrasner',
          imageUrl:
            'https://images.unsplash.com/photo-1519345182560-3f2917c472ef?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
        },
      },
      {
        body: 'Molestias ea earum quos nostrum doloremque sed. Quaerat quasi aut velit incidunt excepturi rerum voluptatem minus harum.',
        author: {
          name: 'Leonard Krasner10',
          handle: 'leonardkrasner',
          imageUrl:
            'https://images.unsplash.com/photo-1519345182560-3f2917c472ef?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
        },
      },
      {
        body: 'Molestias ea earum quos nostrum doloremque sed. Quaerat quasi aut velit incidunt excepturi rerum voluptatem minus harum.',
        author: {
          name: 'Leonard Krasner11',
          handle: 'leonardkrasner',
          imageUrl:
            'https://images.unsplash.com/photo-1519345182560-3f2917c472ef?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
        },
      },
      // More testimonials...
    ],
  ],
]
</script>