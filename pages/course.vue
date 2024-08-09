<template>
  <div class="page-background">
    <div class="container">
      <h1 class="d-flex justify-content-center mb-4 p-3">
        <span class="fs-3">
          Course:
          <span class="fs-3">Mastering Nuxt 3</span>
        </span>
      </h1>
      <div class="row">
        <!-- Chapters Section -->
        <div class="col-md-4 ">
        <div class="bg-white mb-4 p-4 vh-100">
          <h2 class="fs-4 fw-bold">Chapters</h2>
         <div
					class="mt-3"
					v-for="chapter in chapters"
					:key="chapter.slug"
				>
					<h4 class="fs-6">{{ chapter.title }}</h4>
					<NuxtLink
						v-for="(lesson, index) in chapter.lessons"
						:key="lesson.slug"
            class="text-decoration-none d-flex align-items-center mb-2"
           :to="lesson.path"					
					>
						<span class="text-gray-500">{{ index + 1 }}.</span>
						<span class="fs-6 ">{{ lesson.title }}</span>
					</NuxtLink>
				</div>          
        </div>
        </div>
        <!-- Lessons Section -->
        <div class="col-md-8">
        <div class="bg-white  p-4 vh-100">
          <NuxtPage/>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const { chapters } = useCourse();
</script>

<style>
.page-background {
  background-color: #f0f0f0;
  min-height: 100vh; 
}
</style>