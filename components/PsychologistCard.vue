<template>
  <div class="card">
    <img
      v-if="avatarSrc"
      :src="avatarSrc"
      alt="profile image"
      class="card__img"
    />
    <img v-if="avatarSrc" class="img__icon" :src="PlayIcon" alt="play button" />
    <p v-if="name" class="card__name">{{ name }}</p>
    <p v-if="expertise" class="card__expertise">{{ expertise }}</p>
    <p v-if="intro" class="card__intro">{{ intro }}</p>
    <section v-if="availability" class="card__sessions">
      <p class="next-session">{{ DisplayNextSession }}</p>
      <b-container
        ><b-row>
          <b-col
            class="session-time__wrapper"
            cols="4"
            v-for="(t, index) in availability.times"
            :key="_uid + index"
          >
            <button
              v-if="showTime(index)"
              class="btn-styling session-time"
              :class="{ 'session-extra': t.extra }"
            >
              {{ t.time }}
              <span v-if="t.extra"> ({{ t.extra }})</span>
            </button>
            <button
              @click="hideTimes = false"
              class="btn-styling show-more-btn"
              v-else-if="index === 5"
            >
              Show more
            </button>
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
    hideTimes: true,
    PlayIcon
  }),
  props: {
    avatarSrc: {
      type: String,
      default: null
    },
    name: {
      type: String,
      default: null
    },
    expertise: {
      type: String,
      default: null
    },
    intro: {
      type: String,
      default: null
    },
    availability: {
      type: Object,
      default: null
    }
  },
  computed: {
    DisplayNextSession() {
      if (this.availability.nextSession) {
        return `Next sessions on ${this.availability.nextSession}`
      }
      return 'There are no sessions available at the moment'
    }
  },
  methods: {
    showTime(index) {
      if (index < 5 || !this.hideTimes) {
        return true
      }
    }
  }
}
</script>

<style lang="scss" scoped>
@import '~/assets/colours.scss';
.card {
  border: 1px $grey solid;
  min-height: 350px;
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
    left: 55%;
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

      .btn-styling {
        font-family: inherit;
        border: 0;
        padding: 0;
        background: none;
        display: block;
        width: 100%;
      }

      .session-time {
        font-size: 12px;
        background: $primary;
        padding: 7px 0;
        border-radius: 5px;
        margin-bottom: 4px;
        color: $white;

        &:hover {
          background: $secondary;
        }

        &.session-extra {
          background: $secondary;
          padding: 1px 0;
          font-size: 10px;

          span {
            display: block;
          }

          &:hover {
            background: $primary-alt;
          }
        }
      }

      .show-more-btn {
        color: $primary;
        font-size: 11px;

        &:hover {
          color: $secondary;
        }
      }
    }
  }
}
</style>
