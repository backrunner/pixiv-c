<template>
  <div :class="['back2top', showClass ? 'back2top-show' : '']" v-show="show" @click="handleClick">
    <i class="el-icon-top"></i>
  </div>
</template>

<script>
let lastOffset = 0;

export default {
  name: 'Common.BackToTop',
  data() {
    return {
      show: false,
      showClass: false,
    };
  },
  created() {
    window.addEventListener('scroll', this.handleScroll);
  },
  beforeDestroy() {
    window.removeEventListener('scroll', this.handleScroll);
  },
  methods: {
    // event
    hide() {
      if (this.show) {
        this.showClass = false;
        setTimeout(() => {
          this.show = false;
        }, 300);
      }
      lastOffset = window.pageYOffset;
    },
    display() {
      if (!this.show) {
        this.show = true;
        setTimeout(() => {
          this.showClass = this.show;
        }, 0);
      }
    },
    handleScroll() {
      if (window.pageYOffset - lastOffset < -50) {
        this.hide();
      } else if (window.pageYOffset - lastOffset > 100) {
        this.display();
        lastOffset = window.pageYOffset;
      }
    },
    handleClick() {
      window.scrollTo({
        top: 0,
        behavior: 'smooth',
      });
    },
  },
};
</script>
