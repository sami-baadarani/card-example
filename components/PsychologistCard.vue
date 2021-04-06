<template>
  <div class="card">
    <img :src="avatar" alt="profile image" class="card__img" />
    <img class="img__icon" :src="PlayIcon" alt="play button" />
    <p>{{ name }}</p>
    <p>{{ expertise }}</p>
    <p>some text here</p>
    <section></section>
  </div>
</template>

<script>
import PlayIcon from 'assets/icons/play_circle_filled_24dp.svg'
export default {
  name: 'Card',
  data: () => ({
    PlayIcon
  }),
  props: {
    avatar: {
      type: String,
      default: 'https://i.pravatar.cc/'
    },
    name: {
      type: String,
      default: 'Psychologist Name'
    },
    expertise: {
      type: String,
      default: 'Clinical psychologist'
    }
  }
}
</script>

<style lang="scss" scoped>
@import '~/assets/colours.scss';
.card {
  border: 1px $grey solid;
  height: 300px;
  width: 200px;
  position: relative;

  &__img {
    border-radius: 50%;
    width: 100px;
    height: 100px;
    margin: 10px auto;
  }
  .img__icon {
    position: absolute;
    height: 40px;
    width: 40px;
    top: 87px;
    right: 50px;
  }
}
</style>
