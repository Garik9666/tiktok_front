<template>
  <v-container class="mt-5">
    <v-row>
      <div class="text-caption">
        <h1 class="text-center">{{$t('aboutUs')}}</h1>
        <div v-html="text"></div>
      </div>
    </v-row>
  </v-container>
</template>

<script>
    export default {
        name: "aboutUs",
        layout: 'product',
        data(){
            return {
              text: '',
              justifyCenter: 'center',
            }
        },
        async fetch({route, store}) {
          await store.dispatch('brands/fetch');
          // await store.dispatch('wishListAndCart/fetch');
          await store.dispatch('menus/fetch');
          await store.dispatch('pages/getById', [1]);
        },
        async mounted() {
          await this.$store.dispatch('wishListAndCart/fetch');
          // if(this.user){
          //   await this.$store.dispatch('wishListAndCart/getWishListAndCartData', [this.user.id]);
          // }else{
          //   await this.$store.dispatch('wishListAndCart/getWishListAndCartData', [0]);
          // }
          if(this.$i18n.locale === 'am'){
            this.text = this.page.html_am;
          }
          else if(this.$i18n.locale === 'en'){
            this.text = this.page.html;
          }
          else if(this.$i18n.locale === 'ru'){
            this.text = this.page.html_ru;
          }
          console.log(this.page);
        },
        computed: {
          page() {
            return this.$store.getters['pages/page'];
          }
        }
    }
</script>

<style scoped>

</style>
