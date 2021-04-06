<template>
  <section class="page__main">
    <b-container class="main-container">
      <b-row>
        <b-col>
          <h3>Psychologists available</h3>
        </b-col>
      </b-row>
      <b-row>
        <b-col
          v-for="(data, index) in tempData"
          :key="_uid + index"
          class="card-column"
          lg="3"
          md="4"
          sm="6"
          xs="12"
        >
          <card
            :avatarSrc="data.avatarSrc"
            :name="data.name"
            :expertise="data.expertise"
            :intro="data.intro"
            :availability="data.availability"
          />
        </b-col>
      </b-row>
    </b-container>
  </section>
</template>

<script>
import Card from '@/components/PsychologistCard'
import { tempData } from '@/constants/TempData'

export default {
  components: { Card },
  data: () => ({
    tempData
  })
}
</script>

<style lang="scss" scoped>
.page__main {
  .main-container {
    margin-top: 3rem;

    h3 {
      margin-bottom: 24px;
    }

    .card-column {
      margin-bottom: 24px;
    }
  }
}
</style>
