<template>
  <div class="text-center" id="app">
    <h1>Word Translator</h1>
    <h5 class="text-muted">Powered By Vue.js</h5>
    <hr>
    <TranslateForm v-on:formSubmit="translateText"></TranslateForm>
    <TranslateOutput v-text="translatedText"></TranslateOutput>
  </div>
</template>

<script>
import TranslateForm from './components/TranslateForm'
import TranslateOutput from './components/TranslateOutput';

export default {
  name: 'App',
  components: {
    TranslateForm,
    TranslateOutput
  },
  data: function(){
    return {
      translatedText:''
    }
  },
  methods: {
    translateText: function(text, language){
      this.$http.get('https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20211110T000326Z.131e89b2ab082901.373be00bff8416d9aea1fc83775633210398ddae&lang='+language+'&text='+text)
      .then((response) => {
        this.translatedText = response.body.text[0];
      });
    }
  }
}
</script>

<style>
body {
  background:#fefefe;
}
</style>

