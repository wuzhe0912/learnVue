<template lang="pug">
  div.login__wrap
    section.login__container
      div.chat__logo
      div.status__title
        div.status__checkbox(@click="selectName('enterName')" :class="{ isSelected: !nickName }")
          input(type="radio" value="" v-model="name")
          label.checkbox__txt 記住我
        div.status__checkbox(@click="selectName('nickName')" :class="{ isSelected: nickName }")
          input(type="radio" value="匿名" v-model="name")
          label.checkbox__txt 我要匿名
      form.login__form(@submit.prevent="enterMode")
        //- onfocus => 進入焦點時，清空預設文字 onblur => 離開焦點時，恢復預設
        input.form__input.login__input(
          type="text"
          placeholder="請輸入暱稱"
          onfocus="this.placeholder = ''"
          onblur="this.placeholder = '請輸入暱稱'"
          v-model="name"
          :class="{ check__name: feedback }"
        )
        button.btn.login__btn(v-loading="loading") 試玩登入
      footer.login__txt 登入即表明已閱讀並同意
        span.service__txt 服務條款
</template>

<script>
export default {
  name: 'Login',
  data () {
    return {
      name: '',
      feedback: false,
      checked: false,
      nickName: false,
      loading: false
    }
  },

  watch: {
    name (newVal, oldVal) {
      if (newVal !== '') this.feedback = false
    }
  },

  methods: {
    selectName (val) {
      if (val === 'nickName') {
        this.nickName = true
        this.name = '匿名'
      } else {
        this.nickName = false
        this.name = ''
      }
    },

    enterMode () {
      if (this.name) {
        this.$router.push({ name: 'Mode', query: { userName: this.name } })
      } else this.feedback = true
    }
  }
}
</script>

<style lang="scss" scoped>
  @import "./style";
</style>
