<template>
    <div>
        <div class="wrapper">
          <div v-for="todo in todos" :key="todo.id">
            {{ todo.title }}
          </div>          
        </div>
    </div>
</template>

<script>   
  import axios from 'axios';

  export default {
    data(){
      return {
        title: 'todos',
        todos: null,
      }
    },
    // vue-meta 설정
    metaInfo() {
      return {
        // 페이지 제목 설정
        title: this.title,
        // 제목 템플릿 설정: "Vue 앱의 검색엔진 최적화 | yamoo9.gitbook.io/vue-a11y-seo"
        titleTemplate: '%s | yamoo9.gitbook.io/vue-a11y-seo',
        // <html> 요소의 속성 설정
        htmlAttrs: {
          // 주 언어 명시
          lang: 'ko-KR',
          dir: 'ltr'
        },
        // 메타 정보 설정
        meta: [
          { charset: 'utf-8' },
          // SEO 설정
          { name: 'description', content: '페이지 설명', vmid: 'description' },
          { name: 'keywords', content: '페이지, 키워드' },
          { name: 'author', content: '제작자 정보' },
          // SNS 설정
          {
            property: 'og:title',
            content: this.title,
            template: chunk => `${chunk} | yamoo9.gitbook.io/vue-a11y-seo`,
            vmid: 'og:title'
          },
          // 모바일 최적화
          { name: 'viewport', content: 'width=device-width, initial-scale=1' }
        ],
        // 링크 설정
        link: [        
          { rel: 'favicon', href: 'favicon.ico' }
        ]
      }
    },    
    beforeCreate() {      
      var _this = this;
      axios.get('https://jsonplaceholder.typicode.com/todos?_limit=21')
      .then(function (response) {
        _this.todos = response.data;
      })
      .catch(function (error) {
        console.log(error);
      });      
    }
  }
</script>

<style scoped>
.wrapper{
  display:grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 1em;
  grid-row: minmax('100px',auto);
}
.wrapper > div:nth-child(odd){
  background: #eee;  
}
.wrapper > div {
  background: #ddd;  
  padding: 1em;
}

</style>

