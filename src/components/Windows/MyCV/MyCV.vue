<script setup>
import { ref, computed } from 'vue'
import { useLocaleStore } from '@/stores/localeStore'
import ProfileHeader from './ProfileHeader.vue'
import EducationItem from './EducationItem.vue'
import cvData from '@/data/cv-data.json'
import WorkExperienceItem from './WorkExperienceItem.vue'
import ProjectItem from './ProjectItem.vue'
import LanguageItem from './LanguageItem.vue'

const localeStore = useLocaleStore()
const birthdate = new Date(1998, 11, 6) // November 6, 1998 is the month index starting at 0
const today = new Date()
let age = ref(today.getFullYear() - birthdate.getFullYear())

// Adjust age if the current date has not passed the birthdate in the current year
if (today.getMonth() < birthdate.getMonth() || (today.getMonth() === birthdate.getMonth() && today.getDate() < birthdate.getDate())) {
  age.value--
}

const currentLocale = computed(() => localeStore.currentLocale)

// Computed property to get the localized education data
const educationData = computed(() => {
  return cvData[currentLocale.value]?.education || []
})

// Computed property to get the localized work experience data
const experienceData = computed(() => {
  return cvData[currentLocale.value]?.workExperience || []
})

// Computed property to get the localized academic projects data
const projectsData = computed(() => {
  return cvData[currentLocale.value]?.academicProjects || []
})

// Computed property to get the localized languages data
const languagesData = computed(() => {
  return cvData[currentLocale.value]?.languages || []
})
</script>

<template>
  <div class="relative right-0 h-content-window overflow-hidden">
    <div class="w-full h-full bg-white overflow-auto p-2">
      <div>
        <ProfileHeader :age="age" />
        <section class="mt-5">
          <h2 class="font-trebuchet-pixel underline">{{ $t('windows.cv.education') }}</h2>
          <EducationItem v-for="education in educationData" :key="education.id" :education="education" />
        </section>
        <div class="mt-3">
          <h2 class="font-trebuchet-pixel mt-5 underline">{{ $t('windows.cv.proExperience') }}</h2>
          <WorkExperienceItem v-for="(workExperience, index) in experienceData" :key="index" :workExperience="workExperience" />
        </div>
        <div class="mt-3">
          <h2 class="font-trebuchet-pixel mt-5 underline">{{ $t('windows.cv.projects') }}</h2>
          <ProjectItem v-for="(project, index) in projectsData" :key="index" :project="project" />
        </div>
        <div class="mt-3">
          <h2 class="font-trebuchet-pixel mt-5 underline">{{ $t('windows.cv.languages') }}</h2>
          <LanguageItem v-for="(language, index) in languagesData" :key="index" :language="language" />
        </div>
      </div>
    </div>
  </div>
  <a
    rel="noopener"
    :href="'pdf/CV_adem_seddik_' + localeStore.currentLocale + '.pdf'"
    :download="'CV_adem_seddik_' + localeStore.currentLocale + '.pdf'"
    class="absolute bottom-2 right-1 md:right-4 h-6 text-xxs border border-twilight-blue bg-button-submit rounded-sm leading-loose px-3 hover:shadow-button-submit-hover cursor-pointer active:bg-button-clicked"
  >
    {{ $t('buttons.downloadCV') }}
  </a>
</template>
