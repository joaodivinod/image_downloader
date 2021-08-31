<template>
  <section class="container mx-auto downloader pt-10">
  <div class="bg-white mx-auto w-4/5 flex">
    <div class="downloader__imageContent relative h-80 w-80 bg-no-repeat bg-center mx-auto bg-green-600">
      <img src="" alt="">
      <p></p>
    </div>
  </div>


    <button class="button bg-green-600 text-white text-xl" @click="printThis">Baixar</button>
<!--    <button class="button bg-green-600 text-white text-xl" @click="baixarVarias">Baixar Varias Imagens</button>-->

<!--    <div class="flex mt-10 w-4/12 mx-auto rounded-2xl h-60 justify-center items-center bg-blue-600" ref="printcontent">-->
<!--      <p class="text-9xl text-center text-white m-0 p-0">{{valor}}</p>-->
<!--    </div>-->
  </section>
</template>

<script>
import html2canvas from "html2canvas";

export default {
  data() {
    return{
      valor:3,
      bg:''
    }
  },
  methods: {
    async baixarVarias(){
      while (this.valor <= 10) {
        this.valor++;
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
      link.setAttribute("download", "download.png");
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
