<template>
    <v-flex xs12>
        <v-toolbar dark color="primary">
            <v-icon>fas fa-fist-raised</v-icon>
            <v-toolbar-title class="white--text">{{$t('score.casters')}}</v-toolbar-title>
        </v-toolbar>
        <v-flex class="pa-2">
            <v-layout row wrap justify-center align-center>
                <v-btn dark color="teal" v-on:click="swapCaster()">
                    <v-icon left>fas fa-exchange-alt</v-icon>
                    {{$t('score.swap')}}
                </v-btn>
            </v-layout>
        </v-flex>
        <v-flex>
            <v-divider></v-divider>
        </v-flex>
        <v-layout row wrap class="pt-2 pb-2 text-xs-center">
            <v-flex xs6 class="pl-2 pr-2">
                <v-text-field
                    :label="$t('score.CasterName')"
                    v-model="caster1"
                    outline
                ></v-text-field>
                <v-text-field
                    :label="$t('score.CasterTwitter')"
                    v-model="caster1Twitter"
                    outline
                ></v-text-field>
            </v-flex>
            <v-flex xs6 class="pl-2 pr-2">
                <v-text-field
                    :label="$t('score.CasterName')"
                    v-model="caster2"
                    outline
                ></v-text-field>
                <v-text-field
                    :label="$t('score.CasterTwitter')"
                    v-model="caster2Twitter"
                    outline
                ></v-text-field>
            </v-flex>
        </v-layout>
    </v-flex>
</template>
<script>

export default {
  name: 'Casters',
  props: {
    Rep: Object,
    tournament: Object,
  },
  data() {
    return {
      caster1: '',
      caster1Twitter: '',
      caster2: '',
      caster2Twitter: '',
    };
  },
  watch: {
      caster1: function handler(val) {
          this.Rep.Tournament.value.caster[0].displayName = val;
      },
      caster1Twitter: function handler(val) {
          this.Rep.Tournament.value.caster[0].twitter = val;
      },
      caster2: function handler(val) {
          this.Rep.Tournament.value.caster[1].displayName = val;
      },
      caster2Twitter: function handler(val) {
          this.Rep.Tournament.value.caster[1].twitter = val;
      },
  },
  methods: {
    swapCaster() {
        const spareCaster = this.caster2;
        const spareCasterTwitter = this.caster2Twitter;

        this.$set(this, 'caster2', this.caster1);
        this.$set(this, 'caster1', spareCaster);

        this.$set(this, 'caster2Twitter', this.caster1Twitter);
        this.$set(this, 'caster1Twitter', spareCasterTwitter);
    },
  },
  created() {
    this.caster1 = this.Rep.Tournament.value.caster[0].displayName;
    this.caster1Twitter = this.Rep.Tournament.value.caster[0].twitter;
    this.caster2 = this.Rep.Tournament.value.caster[1].displayName;
    this.caster2Twitter = this.Rep.Tournament.value.caster[1].twitter;
  },
};
</script>
<style lang="scss" scoped>
</style>
