<template>
  <v-carousel
    cycle
    :height="sliderMaxWidth"
    :hide-delimiters="true"
    show-arrows-on-hover
    v-resize="onResize"
  >
    <v-carousel-item
      v-for="(slide, i) in slides"
      :key="i"
      :src="slide.src"
      :to="slide.url"
    >

        <v-row
          class="fill-height"
          align="center"
          justify="center"
        >
          <div class="display-3" :style="{color: slide.color}">{{ slide.text }} Slide</div>
        </v-row>

    </v-carousel-item>
  </v-carousel>
</template>


<script>
  export default {
    data () {
      return {
        slides: [
          // {text: 'First', src: '/slider_1.jpg', color: '#ffffff'},
          // {text: 'Second', src: '/slider_2.jpg', color: '#ffffff'},
          // {text: 'Third', src: '/slider_3.jpg', color: '#ffffff'},
        ],
        sliderMaxWidth:  550,
      }
    },
    async mounted () {
      await this.$store.dispatch('components/getComponent', [1]);
      console.log(this.component);
      this.onResize();
      if(this.slides.length == 0 && this.component.length !== 0){
        this.component.componentElements.forEach((el) => {
          this.slides.push({text: el.name, src: el.image, url: el.url});
        })
      }
    },
    methods: {
      onResize () {
        if(window.innerWidth <= 960){
          this.sliderMaxWidth = 350;
        }else{
          this.sliderMaxWidth = 550;
        }
        this.windowSize = { x: window.innerWidth, y: window.innerHeight }
      },
    },
    computed: {
      component() {
        return this.$store.getters['components/slider'];
      },
    },
  }
</script>
