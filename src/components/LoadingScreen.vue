<template>
  <div class="loader">
    <div class="load-text">
      <div class="loaded-text">Events</div>
      <div class="loading-text">App</div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'LoadingScreen',
  }
</script>

<style lang="scss" scoped>
  .loader {
    position: fixed;
    left: 0;
    top: 0;
    background: white;
    width: 100%;
    height: 100vh;
    animation: backgroundChange .5s linear 3s forwards, fadeOut .5s linear 5s forwards
  }

  .load-text {
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    position: absolute;
    font-size: 5vmax;
    width: fit-content;
    display: flex;
    animation: colorChange .5s linear 3s forwards;
  }

  .loaded-text {
    transform: scale(1.5);
    animation: scaleText .5s linear .5s forwards;
  }

  .loading-text {
    width: 0;
    overflow: hidden;
    animation: expand .5s linear 1.5s forwards;
  }

  main {
    padding: 1em;
    box-sizing: border-box;
    background-color: #1976D2;
    color: white;
    min-height: 100vh;
    font-family: 'Open Sans', sans-serif;
  }

  @keyframes scaleText {
    from {transform: scale(1.5)}
    to {transform: scale(1)}
  }

  @keyframes expand {
    from {width: 0;}
    to {width: 11vmax;}
  }

  @keyframes backgroundChange {
    from {background-color: white}
    to {background-color: #1976D2}
  }

  @keyframes colorChange {
    from {color: #1976D2}
    to {color: white}
  }

  @keyframes fadeOut {
    from {opacity: 1}
    to {
      opacity: 0;
      z-index: -1;
    }
  }
</style>
