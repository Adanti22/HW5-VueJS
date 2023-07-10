<script>
/* 1. Сделать директиву, которая в качестве значения принимает объект со свойствами: массив из ссылок, которые добавляются в image, и промежуток, через который сменится ссылка у картинки.
Добавить модификаторы, которые позволяют менять картинку на случайную из массива.
 */

export default {
  data() {
    return {
      obj: {
        currIndex: 0,
        prevIndex: "",
        arr: [
          "https://mir-znaniy.com/wp-content/uploads/2017/01/neptun-most.jpg",
          "https://ichef.bbci.co.uk/news/640/amz/worldservice/live/assets/images/2014/09/03/140903105827_uranus_space_624x351_spl.jpg",
          "https://starwalk.space/gallery/images/saturn-planet-guide/1140x641.jpg",
          "https://avatars.dzeninfra.ru/get-zen_doc/59919/pub_5ab53bef20ea2b5abbfcd6e9_5ab53c1c8c8be3aefcebfe88/scale_1200",
          "https://starwalk.space/gallery/images/mars-the-ultimate-guide/1920x1080.jpg",
          "https://cdnn1.img.sputnik.tj/img/07e5/03/0c/1032994480_244:0:1684:1080_1920x0_80_0_0_d53fc6453c122d764649de23e77af005.jpg",
          "https://icdn.lenta.ru/images/2022/11/15/11/20221115112851877/square_320_6301b2ea9e452dc99b8642b4baa6fa5e.jpeg",
          "https://news.store.rambler.ru/img/60547c1388fc215f65780c38fba6e9a3?img-format=auto&img-1-resize=height:400,fit:max&img-2-filter=sharpen",
        ],
        interval: 1123,
      },
    };
  },

  directives: {
    dirr: {
      mounted(el, binding) {
        console.log(binding.value.arr);
        setInterval(() => {
          if (binding.modifiers.random) {
            let randomIndex = Math.floor(
              Math.random() * binding.value.arr.length
            );
            if (binding.value.prevIndex === randomIndex) {
              if (binding.value.arr.length === randomIndex + 1) randomIndex--;
              else randomIndex++;
            }
            binding.value.prevIndex = randomIndex;
            console.log(randomIndex);
            el.setAttribute("src", binding.value.arr[randomIndex]);
          } else {
            el.setAttribute("src", binding.value.arr[binding.value.currIndex]);
            if (binding.value.arr.length - 1 == binding.value.currIndex) {
              binding.value.currIndex = 0;
            } else {
              binding.value.currIndex++;
            }
          }
        }, binding.value.interval);
      },
      updated(el, binding) {
        console.log(binding.value);
      },
    },
  },
};
</script>

<template>
  <div class="container">
    <img src="" alt="" class="earth" v-dirr.random="obj" />
  </div>
</template>

<style scoped>
.earth {
  width: 30vw;
  height: 30vw;
  object-fit: contain;
}
button {
  width: 30vw;
  height: 5vh;
  cursor: pointer;
  font-size: 20px;
}
</style>
