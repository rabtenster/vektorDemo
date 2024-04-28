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

      // This position we might need to get from the IFC - unclear
      const position = [24.91781, 60.15555, -90.7];
      const altitude = 0;

      const ve = new VektorEmbedded();
      await ve.init(true)
      ve.mount(sessionToken, divId, {
          enableContextMenu: true,
          enableMarkup: true,
          enableClippingPlanes: true,
          enableMeasuring: true,
          useLightMap: true,
          drawModelsOnTopOfMap: true,
          isElementSelectionLimitedToRooms: false,
        },
        // Path to room information
        {
            path: [], // use all props
            roomIdentifier: ['Ifc-Name'],
            roomNumber: ['Ifc-Name'],
            extra: {
                roomName: ['Ifc-Name'],
            },
        }
      );
      // const vek = new VektorEmbeddedBasic(sessionToken, divId);
      // const vek = await VektorEmbeddedBasic.create(sessionToken, divId);
      // console.log("base =", vek);

      const showMapLayer = (layerName) => {
        ve.getWmsLayers('https://kartta.hel.fi/ws/geoserver/avoindata/wms').then((layers) => {
          for (let item of layers) console.log(item.title);
          const layer = layers.find((item) => item.title === layerName);
          console.log("Found map layer", layer);
          return ve.addMapLayer(layer.id);
        });
      };

      await ve.setTerrain('FINLAND_10M');
      await ve.addModel(modelId, coordinateSystem)

      console.log("Showing map layer");
      // showMapLayer('Ortoilmakuva');


      ve.flyToModel(modelId);

    },
  }
}
</script>

<style>

</style>