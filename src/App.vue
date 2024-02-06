<script setup>
  const sessionToken = '7b70078fa1573627b9403cd8842cdb08823c03043ca8be5d0a86e957a491be96';
  const divId = 'vektorioContainer';
  const vektorEmbedded = await VektorEmbeddedBasic.create(
      sessionToken,
      divId
  );
  const modelId = 'ca1fc12d33f635cda586e025b27ee0d571b1a3ce42e98e779afe84e966b6ee2c';
  const coordinateSystem = {
        originPositionX: null,
        originPositionY: null,
        originPositionZ: null,
        originPositionRotationZ: null,};
  await vektorEmbedded.addModel(modelId, coordinateSystem);
  vektorEmbedded.flyToModel(modelId);
</script>

<template>
   <Suspense>
    <div id="vektorioContainer"></div>
  </Suspense>
</template>

<style scoped>

</style>
