<template class="relative">
  <section class="mx-auto downloader pt-10 flex flex-col">

  <div class="bg-white mx-auto downloader--Dlcontainer h-80 flex rounded-2xl w-4/5 flex relative">
    <img @click="showConfig = true" class="absolute -right-5 -top-3 cursor-pointer" src="~/assets/img/icons/gears.svg" alt="">

    <div class="downloader__imageContent relative h-80 w-80 bg-no-repeat bg-center m-auto relative"
         ref="printcontent" >
      <p class="gotham-black text-white absolute right-4 bottom-10 text-3xl">{{ valorInicial }}</p>
    </div>


  </div>

    <div class="downloader--Dlcontainer mx-auto my-5 flex justify-between" >

      <h2 class="text-center" v-if="downloadType" >Baixar Varias</h2>
      <h2 class="text-center" v-else>Baixar Apenas Uma</h2>

      <label class="switch">
        <input type="checkbox" v-model="downloadType">
        <span class="slider round"></span>
      </label>

    </div>

    <div v-if="downloadType" class="downloader--Dlcontainer  mx-auto downloader__values">

     <div class="flex justify-between text-center">
       <input v-model.number="valorInicial" type="number" min="0" max="1500" placeholder="De" class="w-5/12 rounded-xl px-3">
       <div class="w-px bg-gray-300 h-10"></div>
       <input v-model.number="valorFinal" type="number" min="0" max="1500" placeholder="Até" class="w-5/12 rounded-xl px-3">
     </div>

      <button class="mt-7 downloader__buttonDownload text-white w-full rounded-xl h-12" @click="baixarVarias">Baixar Varias Imagens</button>

    </div>

    <div v-else class="downloader--Dlcontainer  mx-auto downloader__values">

      <div class="flex justify-between text-center">
        <input v-model.number="valorInicial" type="number" min="0" max="1500" placeholder="Número do grupo" class="w-7/12 rounded-xl px-3">

        <div class="w-px bg-gray-300 h-10"></div>

        <div class="flex justify-between text-center w-4/12 ">
          <button class="bg-green-500 rounded-xl w-5/12 h-full bg-opacity-80" @click="valorInicial +=1 " >
            <span class="text-2xl text-green-800 mb-5">+</span>
          </button>
          <button class="bg-red-500 rounded-xl w-5/12 h-full bg-opacity-80 " @click="valorInicial -=1 " >
            <span class="text-2xl text-red-800 mb-5">-</span>
          </button>
        </div>
      </div>

      <button class="mt-7 downloader__buttonDownload text-white w-full rounded-xl h-12"  @click="printThis">Baixar Apenas Uma</button>

    </div>

    <section v-show="showConfig" class="imageSelection min-h-screen absolute top-0 flex flex-col w-full">
        <div class="bg-white p-20 my-20 w-11/12 mx-auto rounded-2xl shadow-xl relative">

          <button @click="showConfig = false" class="absolute -right-3 -top-3 shadow bg-red-300 w-12 h-12 rounded-xl flex justify-center items-center" >
            <svg xmlns="http://www.w3.org/2000/svg" width="12.828" height="12.828" viewBox="0 0 12.828 12.828">
              <g id="x" transform="translate(1.414 1.414)">
                <path id="Path" d="M10,0,0,10" fill="none" stroke="#ce0000" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width="2"/>
                <path id="Path-2" data-name="Path" d="M0,0,10,10" fill="none" stroke="#ce0000" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width="2"/>
              </g>
            </svg>
          </button>

          <h1 class="text-2xl text-gray-700 ">Escolha uma nova imagem de perfil</h1>

          <div class="flex  flex-wrap">
            <div class="w-2/12 mx-5 mt-10" v-for="index in 8" :key="index">
              <img class="" :src='`/_nuxt/assets/img/profile-pics/profilepic${index}.png`' alt="">
<!--              <img class="" src='~/assets/img/profile-pics/profilepic1.png' alt="">-->
              <button class="mt-7 downloader__buttonDownload text-white w-full rounded-xl h-12">Selecionar</button>
            </div>
          </div>

        </div>
    </section>

  </section>

</template>

<script>
import html2canvas from "html2canvas";

export default {
  data() {
    return{
      valorInicial:null,
      valorFinal:null,
      lancamento:'MasterLove',
      downloadType:true,

      grupCover:'profilepic1.png',

      showConfig:true
    }
  },
  methods: {
    async baixarVarias(){
      while (this.valorInicial <= this.valorFinal) {
        this.valorInicial++;
        await this.printThis()

      }
    },

    async printThis() {
      console.log("printing..");
      const el = this.$refs.printcontent;

      const options = {
        type: "dataURL"
      };
      const printCanvas = await html2canvas(el, options);

      const link = document.createElement("a");

      if (this.downloadType){
        link.setAttribute("download", this.lancamento + (this.valorInicial -1)  + ".png");
      }
        else{
          link.setAttribute("download", this.lancamento + this.valorInicial + ".png");
        }


      link.setAttribute(
        "href",
        printCanvas
          .toDataURL("image/png")
          .replace("image/png", "image/octet-stream")
      );
      link.click();

      console.log("done");
    },


  },
}
</script>

<style lang="scss">
  .imageSelection{
    background-color: #EAF2FF;
  }
</style>
