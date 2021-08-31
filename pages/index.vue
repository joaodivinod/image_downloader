<template>
  <section class="container mx-auto downloader pt-10 flex flex-col">

  <div class="bg-white mx-auto downloader--Dlcontainer h-80 flex rounded-2xl w-4/5 flex">
    <div class="downloader__imageContent relative h-80 w-80 bg-no-repeat bg-center m-auto bg-green-600 relative" ref="printcontent">
<!--      <img class="absolute w-28 left-4 bottom-8" src="static/img/logo-master-love.png" alt="">-->
      <p class="gotham-black text-white absolute right-4 bottom-7 text-3xl">{{ valorInicial }}</p>
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
      downloadType:true
    }
  },
  methods: {
    async baixarVarias(){
      while (this.valorInicial <= this.valorFinal) {
        await this.printThis()
        this.valorInicial++;
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
      link.setAttribute("download", this.lancamento + this.valorInicial + ".png");
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
