<script setup>
import { watch, ref } from 'vue';
import Search from '../../components/Search/index.vue';
import Card from '../../components/Card/index.vue';

const urlPosts = 'http://jsonplaceholder.typicode.com/posts';
const urlAutors = 'http://jsonplaceholder.typicode.com/users';
const postsList = ref([]);
const authorsList = ref([]);
const searchValue = ref(null);
const filteredPosts = ref([]);

Promise.all
  ([
      fetch(urlPosts).then(response => response.json()),
      fetch(urlAutors).then(response => response.json())
  ])
  .then(data => {
      postsList.value = data[0],
      authorsList.value = data[1]
      mergeData()
      filteredPosts.value = postsList.value
  })
  .catch(error => {
      console.log('Ошибочка' + error)
  });

// Добавляем автора в соответствии с id
function mergeData() {
  for (let i = 0; i < postsList.value.length; i++) {
    let author = authorsList.value.find(author => author.id === postsList.value[i].userId)
    postsList.value[i]['author'] = author.name
  }
};

// Фильтрация массива
watch(searchValue, () => {
  if (searchValue.value) filteredPosts.value = postsList.value.filter(post => post.author.toLowerCase().includes(searchValue.value.toLowerCase()))
  if (!searchValue.value) filteredPosts.value = postsList.value
});

</script>

<template>
    <div class="home">
        <Search 
          class="home__search"
          v-model="searchValue"
          placeholder="filter by author..."
        />
        <div class="home__container">
          <Card 
              v-for="post in filteredPosts"
              :key="post.id"
              :title="post.title"
              :text="post.body"
              :author="post.author"
          />
          <div class="home__notification" v-if="!filteredPosts.length">Ничего не найдено</div>
        </div>
    </div>
</template>

<style lang="scss" scoped>
  @import './styles/home.scss';
</style>