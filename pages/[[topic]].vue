<script lang="ts" setup>

const route = useRoute()
const { topic } = route.params

const capitalizeFirstLetter = (word: string): string => {
    if (word.length < 3) {
        return word
    }
    if (!word[0].match(/[a-zA-Z]/i)) {
        return word
    }
    return word[0].toUpperCase() + word.slice(1)
}

const generateCapitalizedString = (text: string) => {
    const words = text.split("-")
    for (let i = 0; i < words.length; i++) {
        words[i] = capitalizeFirstLetter(words[i])
    }
    return words.join(" ")
}

const topicString = computed(() => {
    if (Array.isArray(topic)) {
        return topic.join("-")
    }
    return topic
})

useSeoMeta({
  title: generateCapitalizedString(topicString.value),
  description: "",
})
</script>

<template>
  <main class="text-center">
    <section class="space-y-4 my-32">
      <h1 class="text-6xl md:text-9xl font-bold text-center">{{ generateCapitalizedString(topicString) }}</h1>
      <p class="italic">Did you want a source related to "{{ generateCapitalizedString(topicString) }}"? Nah, just trust me bro!</p>
    </section>
    <section>
      <article class="text-center space-y-3">
        <h3 class="text-3xl">Did someone use this link as a source during a discussion or argument?</h3>
        <p class="text-xl">That means that they need you to trust them on this one!</p>
        <p>
          Scholarly sources are great, but so is having the confidence to state an opinion based on a surface-level understanding of a topic.
        </p>
      </article>
    </section>
  </main>
</template>

<style scoped></style>
