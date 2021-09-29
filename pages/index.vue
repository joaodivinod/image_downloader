<template class="relative z-0">
   <section class="mx-auto downloader pt-10 flex flex-col">
      <div class="bg-white mx-auto downloader--Dlcontainer h-80 flex rounded-2xl w-4/5 flex relative">
         <img @click="showConfig = true" class="absolute -right-5 -top-3 cursor-pointer"
              src="~/assets/img/icons/gears.svg"
              alt="">
         <div
            :class="`downloader__imageContent relative h-80 w-80 bg-no-repeat bg-center m-auto relative
            ${colorPickerBackground.gradient ? 'bg-gradient-to-r from-' + colorPickerBackground.primary
             + ' to-' + colorPickerBackground.secondary : 'bg-' + colorPickerBackground.primary} `"
            ref="printcontent">
            <p class="gotham-black text-white absolute right-4 bottom-10 text-3xl">{{ valorInicial }}</p>
            <img :src="require(`~/assets/img/profile-pics/profilepic${groupCover}.png`)" alt=""/>
         </div>
      </div>

      <div class="mx-auto flex text-center justify-around lg:w-3/12 w-full flex relative my-4 p-4">
         <div class="w-1/2 flex justify-around">
            <div class="w-4/12" @click="colorPickerBackground.show = true">
               <div class="bg-white rounded-2xl p-3 w-min mx-auto cursor-pointer transition-all shadow hover:shadow-xl">
                  <div :class="`h-10 w-10 rounded bg-${colorPickerBackground.primary}`"></div>
               </div>
               <p class="mt-2 text-lg">Fundo</p>
            </div>
            <div class="w-4/12 flex flex-col items-center justify-center">
               <label class="switch">
                  <input type="checkbox" v-model="colorPickerBackground.gradient">
                  <span class="slider round"></span>
               </label>
               <span class="text-center">Gradiente</span>
            </div>
         </div>
         <div class="absolute pt-2 top-0 left-20 z-10 transition-all" v-if="colorPickerBackground.show">
            <div class="relative bg-white border border-gray-200 rounded-md shadow-xl p-4">
               <div class="flex-1 grid grid-cols-6 2xl:grid-cols-8 gap-x-4 gap-y-3 2xl:gap-x-2">
                  <div v-for="color in colorOptions"
                       :class="`h-10 w-10 border-${selectedColor === color ? '2' : '0'} border-solid border-black transition-all shadow hover:shadow-xl cursor-pointer transform
                        hover:-translate-y-1 rounded bg-${color}`" @click="selectColor(color)"/>
               </div>
               <div class="w-full mt-4 flex justify-around">
                  <button v-if="colorPickerBackground.gradient" class="bg-blue-500 text-white rounded-xl py-1 px-5"
                          @click="colorPickerBackground.primary = selectedColor">
                     Primária
                  </button>
                  <button v-if="colorPickerBackground.gradient" class="bg-blue-500 text-white rounded-xl py-1 px-5"
                          @click="colorPickerBackground.secondary = selectedColor">
                     Secundária
                  </button>
                  <button class="bg-indigo-800 text-white rounded-xl py-1 px-5"
                          @click="colorPickerBackground.show = false">
                     Fechar
                  </button>
               </div>
            </div>
         </div>
      </div>

      <div class="downloader--Dlcontainer mx-auto my-5 flex justify-between">
         <h2 class="text-center" v-if="downloadType">Baixar Varias</h2>
         <h2 class="text-center" v-else>Baixar Apenas Uma</h2>

         <label class="switch">
            <input type="checkbox" v-model="downloadType">
            <span class="slider round"></span>
         </label>

      </div>

      <div v-if="downloadType" class="downloader--Dlcontainer  mx-auto downloader__values">

         <div class="flex justify-between text-center">
            <input v-model.number="valorInicial" type="number" min="0" max="1500" placeholder="De"
                   class="w-5/12 rounded-xl px-3">
            <div class="w-px bg-gray-300 h-10"></div>
            <input v-model.number="valorFinal" type="number" min="0" max="1500" placeholder="Até"
                   class="w-5/12 rounded-xl px-3">
         </div>

         <button class="mt-7 downloader__buttonDownload text-white w-full rounded-xl h-12" @click="baixarVarias">
            Baixar Varias Imagens
         </button>
      </div>

      <div v-else class="downloader--Dlcontainer  mx-auto downloader__values">

         <div class="flex justify-between text-center">
            <input v-model.number="valorInicial" type="number" min="0" max="1500" placeholder="Número do grupo"
                   class="w-7/12 rounded-xl px-3">

            <div class="w-px bg-gray-300 h-10"></div>

            <div class="flex justify-between text-center w-4/12 ">
               <button class="bg-green-500 rounded-xl w-5/12 h-full bg-opacity-80" @click="valorInicial +=1 ">
                  <span class="text-2xl text-green-800 mb-5">+</span>
               </button>
               <button class="bg-red-500 rounded-xl w-5/12 h-full bg-opacity-80 " @click="valorInicial -=1 ">
                  <span class="text-2xl text-red-800 mb-5">-</span>
               </button>
            </div>
         </div>

         <button class="mt-7 downloader__buttonDownload text-white w-full rounded-xl h-12" @click="printThis">
            Baixar Apenas Uma
         </button>

      </div>

      <section v-show="showConfig" class="imageSelection min-h-screen absolute top-0 flex flex-col w-full">
         <div class="bg-white md:p-20 p-5 my-20 w-11/12 mx-auto rounded-2xl shadow-xl relative">
            <button @click="showConfig = false"
                    class="absolute -right-3 -top-3 shadow bg-red-300 md:w-12 md:h-12 w-8 h-8 rounded-xl flex justify-center items-center">
               <svg xmlns="http://www.w3.org/2000/svg" width="12.828" height="12.828" viewBox="0 0 12.828 12.828">
                  <g id="x" transform="translate(1.414 1.414)">
                     <path id="Path" d="M10,0,0,10" fill="none" stroke="#ce0000" stroke-linecap="round"
                           stroke-linejoin="round"
                           stroke-miterlimit="10" stroke-width="2"/>
                     <path id="Path-2" data-name="Path" d="M0,0,10,10" fill="none" stroke="#ce0000"
                           stroke-linecap="round"
                           stroke-linejoin="round" stroke-miterlimit="10" stroke-width="2"/>
                  </g>
               </svg>
            </button>
            <h1 class="md:text-2xl text-base text-gray-700 ">Escolha uma nova imagem de perfil</h1>
            <div class="flex flex-wrap">
               <div class="md:w-2/12 w-8/12 md:mx-5 mx-auto mt-10 relative" v-for="index in 4" :key="index">
                  <img :src="require(`~/assets/img/profile-pics/profilepic${index}.png`)" alt="">
                  <!--              <button @click="groupCover = index"-->
                  <!--                      class="mt-7 downloader__buttonDownload text-white w-full rounded-xl h-12"-->
                  <!--                      :class="index === groupCover ? 'downloader__buttonDownload&#45;&#45;select' : null ">-->
                  <!--                      <span v-if="index === groupCover">Selecionada</span>-->
                  <!--                      <span v-else>Selecionar</span>-->
                  <!--              </button>-->

                  <button @click="groupCover = index"
                          class="mt-7 downloader__buttonDownload text-white absolute -top-4 right-3 w-6 h-6 rounded-full"
                          :class="index === groupCover ? 'downloader__buttonDownload--select' : null ">
                     <span v-if="index === groupCover">✓</span>
                     <span v-else class="">◯</span>
                  </button>
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
      return {
         valorInicial: null,
         valorFinal: null,
         lancamento: 'MasterLove',
         downloadType: true,
         groupCover: 1,
         showConfig: false,
         colors: ['gray', 'red', 'green', 'yellow', 'blue', 'indigo', 'purple',
            'pink'],
         colorOptions: [],
         colorPickerBackground: {primary: 'transparent', secondary: '', show: false, gradient: true},
         selectedColor: ''
      }
   },
   async created() {
      //Preparando cores
      await this.colors.forEach(color => {
         for (let i = 100; i < 900; i += 100) {
            this.colorOptions.push(color + '-' + i)
         }
      })
   },
   methods: {
      async baixarVarias() {
         while (this.valorInicial <= this.valorFinal) {
            this.valorInicial++;
            await this.printThis()
         }
      },

      async printThis() {
         console.log("printing..");
         const el = this.$refs.printcontent;

         const options = {
            type: "dataURL",
         };

         const printCanvas = await html2canvas(el, options);

         const link = document.createElement("a");

         if (this.downloadType) {
            link.setAttribute("download", this.lancamento + (this.valorInicial - 1) + ".png");
         } else {
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
      selectColor(value) {
         this.selectedColor = value
         if(!this.colorPickerBackground.gradient)
            this.colorPickerBackground = {primary: value, secondary: '', show: false}
      },
   },
}
</script>

<style lang="scss" scoped>
.imageSelection {
   background-color: #EAF2FF;
}
.bg-gradient-to-r {
   background-image: linear-gradient(35deg, var(--tw-gradient-stops));
}
</style>
