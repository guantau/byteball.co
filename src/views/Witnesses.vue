<template>
  <div>
    <div class="container-md p-responsive">
      <h1 class="py-8 text-center">Witnesses</h1>
    </div>
    <ul class="container-md p-responsive">
      <MessageLoading v-if="witnesses.length === 0"/>
      <li v-for="(witness, i) in witnesses" class="d-block width-full py-4 clearfix border-bottom">
        <div class="flex-content-start mb-1">
          <router-link :to="'/@' + witness">
            <span class="float-left mr-3">
              <Avatar size="44" :address="witness"/>
            </span>
          </router-link>
          <div>
            <router-link :to="'/@' + witness" class="mr-1">
              {{witness}}
            </router-link>
          </div>
        </div>
        <div class="d-flex">
          <div>
            <p>#{{i + 1}}</p>
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import { mapActions } from 'vuex';

export default {
  computed: {
    witnesses () {
      return this.$store.state.app.witnesses || [];
    },
  },
  methods: mapActions([
    'getWitnesses',
  ]),
  created() {
    if (this.$store.state.app.witnesses.length === 0) {
      this.getWitnesses();
    }
  }
}
</script>
