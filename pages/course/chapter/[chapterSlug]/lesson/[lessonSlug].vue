<template>
  <p class="fw-bold">Lesson {{ chapter.number }} - {{ lesson.number }}</p>
  <h2 class="fs-5 fw-bold">{{ lesson.title }}</h2>
<NuxtLink
				v-if="lesson.sourceUrl"
				class="font-normal text-gray-500 text-md"
				:to="lesson.sourceUrl"
			>
				Download Source Code
			</NuxtLink>
  <NuxtLink
    v-if="lesson.downloadUrl"
    class="font-normal text-gray-500 text-md"
    :to="lesson.downloadUrl"
  >
    Download Video </NuxtLink
  ><VideoPlayer v-if="lesson.videoId" :video-id="lesson.videoId" />
  <p>{{ lesson.text }}</p>
<LessonCompleteButton
			:model-value="isLessonComplete"
			@update:model-value="toggleComplete"
		/></template>

<script setup>
const course = useCourse();
const route = useRoute();

const chapter = computed(() => {
  return course.chapters.find(
    (chapter) => chapter.slug === route.params.chapterSlug
  );
});

const lesson = computed(() => {
  return chapter.value.lessons.find(
    (lesson) => lesson.slug === route.params.lessonSlug
  );
});

const title = computed(() => {
	return `${lesson.value.title} - ${course.title}`;
});

useHead({
	title,
});

const progress = useLocalStorage('progress', []);

const isLessonComplete = computed(() => {
	if (!progress.value[chapter.value.number - 1]) {
		return false;
	}

	if (!progress.value[chapter.value.number - 1][lesson.value.number - 1]) {
		return false;
	}

	return progress.value[chapter.value.number - 1][lesson.value.number - 1];
});

const toggleComplete = () => {
	if (!progress.value[chapter.value.number - 1]) {
		progress.value[chapter.value.number - 1] = [];
	}

	progress.value[chapter.value.number - 1][lesson.value.number - 1] =
		!isLessonComplete.value;
};
</script>
