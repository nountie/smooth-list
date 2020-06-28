<template>
  <li><b>{{index+1}}.</b><span class="content" v-html="content"></span></li>
</template>

<script>
export default {
  name: 'ToDo',
  props: {
    content: {
      required: true,
      type: String
    },
    index: {
      type: Number
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

b {
  margin-right: 5px;
}
li {
  transition: all 0.3s ease-in-out;
  text-align: left;
  color: #666666;
  padding: 15px 20px;
  margin: 0px 0px;
  border-bottom: 1px solid #eee;
  background: #fff;
  position: relative;
  display: inline-block;
  min-width: 100%;
}
li::before {
  content: "";
  display: block;
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
 box-shadow:
  0 2.8px 2.2px rgba(39, 47, 58, 0.011),
  0 6.7px 5.3px rgba(39, 47, 58, 0.016),
  0 12.5px 10px rgba(39, 47, 58, 0.02),
  0 22.3px 17.9px rgba(39, 47, 58, 0.024),
  0 41.8px 33.4px rgba(39, 47, 58, 0.029),
  0 100px 80px rgba(39, 47, 58, 0.04);
  z-index: -1;
}
a {
  color: #42b983;
}


.compress-move {
    transition: all .3s ease-in-out;
}

.compress-enter-active {
    transition: all .3s ease-in-out;
}

.compress-enter {
    transform: scale(0.92) translatey(-30px);
    transform-origin: top center;
    opacity: 0;
}

.compress-leave-to {
    transform: translatey(30px) scale(0.9);
    opacity: 0;
}

.compress-leave-active {
    transition: all .3s ease-in-out;
    position: absolute;
    left: 0px;
}

</style>
