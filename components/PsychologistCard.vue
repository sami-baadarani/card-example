<template>
  <div class="card">
    <img :src="avatarSrc" alt="profile image" class="card__img" />
    <img class="img__icon" :src="PlayIcon" alt="play button" />
    <p class="card__name">{{ name }}</p>
    <p class="card__expertise">{{ expertise }}</p>
    <p class="card__intro">{{ intro }}</p>
    <section class="card__sessions">
      <p class="next-session">{{ DisplayNextSession }}</p>
      <b-container
        ><b-row>
          <b-col
            class="session-time__wrapper"
            cols="4"
            v-for="(t, index) in availability.times"
            :key="_uid + index"
          >
            <div class="session-time" :class="{ 'session-extra': t.extra }">
              {{ t.time }}
              <span v-if="t.extra"> ({{ t.extra }})</span>
            </div>
          </b-col>
        </b-row>
      </b-container>
    </section>
  </div>
</template>

<script>
import PlayIcon from 'assets/icons/play_circle_filled_24dp.svg'
export default {
  name: 'Card',
  data: () => ({
    showMore: false,
    PlayIcon
  }),
  props: {
    avatarSrc: {
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
    },
    intro: {
      type: String,
      default: `Lorem ipsum dolor sit amet, consectetur adipiscing elit. sed do eiusmod tempor incididunt.`
    },
    availability: {
      type: Object,
      default: {
        nextSession: 'Tuesday 6th Apr',
        times: [
          { time: '8am', extra: '+$25' },
          { time: '9am' },
          { time: '10am' },
          { time: '11:30am' },
          { time: '12:30am' },
          { time: '1:00pm' },
          { time: '2:00pm' }
        ]
      }
    }
  },
  mounted() {
    console.log(this._uid)
  },
  computed: {
    DisplayNextSession() {
      if (this.availability.nextSession) {
        return `Next sessions on ${this.availability.nextSession}`
      }
      return 'There are no sessions available at the moment'
    }
  }
}
</script>

<style lang="scss" scoped>
@import '~/assets/colours.scss';
.card {
  border: 1px $grey solid;
  min-height: 350px;
  //todo remove width
  width: 200px;
  position: relative;
  text-align: center;
  padding: 4px;

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

  &__name {
    color: $text;
    margin-top: 6px;
    margin-bottom: 0;
  }

  &__expertise {
    color: $primary;
    font-size: 12px;
    margin-top: 5px;
    margin-bottom: 0;
  }

  &__intro {
    color: $text;
    font-size: 10px;
    margin-top: 2px;
  }

  .card__sessions {
    .next-session {
      font-size: 12px;
      margin-bottom: 8px;
    }

    .session-time__wrapper {
      padding-right: 5px;
      padding-left: 5px;

      .session-time {
        font-size: 12px;
        background: $primary;
        padding: 7px 0;
        border-radius: 5px;
        margin-bottom: 4px;
        color: $white;

        &.session-extra {
          background: $secondary;
          padding: 1px 0;
          font-size: 10px;

          span {
            display: block;
          }
        }
      }
    }
  }
}
</style>
