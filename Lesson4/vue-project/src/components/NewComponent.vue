<!-- Создайте компонент галереи изображений, который будет отображать одно большое изображение и под ним
будет находиться три мини изображения, при клике на любое минни изображение оно будет отображаться вместо 
большого изображения -->


<template>
    <div id="app">
        <div>
            <img :src="currentImg" alt="image" />
        </div>
        <div v-for="(image, index) in images" :key="index">
            <img @click="changeImg(index)" :src="image" alt="image" />
        </div>
    </div>
</template>
  
<script>
export default {

    data() {
        return {
            images: [
                'https://i1.sndcdn.com/avatars-000500880357-y0evud-t500x500.jpg',
                'https://i1.sndcdn.com/avatars-000285363275-nbosup-t500x500.jpg',
                'https://i.pinimg.com/736x/8f/f8/98/8ff898e172fff315801491dc63795f99--funny-cat-pics-funny-cats.jpg'
            ],
            currentIndex: 0,
        };
    },

    methods: {
        changeImg(index) {
            this.currentIndex = index;
        }
    },

    computed: {
        currentImg() {
            return this.images[this.currentIndex];
        }
    }
};
</script>
  
<style lang="scss" scoped>
#app {
    font-family: Arial, Helvetica, sans-serif;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
</style>