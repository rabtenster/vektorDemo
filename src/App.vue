<template>
  <div id="vektorioContainer" class="vektorContainer"></div>
</template>

<script>
import VektorEmbeddedBasic from 'vektor-embedded';

export default {
  name: 'App',
  data() {
    return {
    }
  },

  mounted() {
    this.loadVektorEmbedded();
  },
  methods: {
    async loadVektorEmbedded() {
      const sessionToken = '7b70078fa1573627b9403cd8842cdb08823c03043ca8be5d0a86e957a491be96';
      const divId = 'vektorioContainer';
      const modelId = 'ca1fc12d33f635cda586e025b27ee0d571b1a3ce42e98e779afe84e966b6ee2c';
      const coordinateSystem = 'ForceZeroOrigin';

      const ve = new VektorEmbedded();
      await ve.init(true)
      ve.mount(sessionToken, divId);
      // const vek = new VektorEmbeddedBasic(sessionToken, divId);
      // const vek = await VektorEmbeddedBasic.create(sessionToken, divId);
      // console.log("base =", vek);
      await ve.addModel(modelId, coordinateSystem)
      ve.flyToModel(modelId);

    }
  }
}
</script>

<style>

</style>