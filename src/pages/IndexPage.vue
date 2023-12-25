<template>
  <q-page>
    <q-page>
      <p class="text-h6 text-center">Bar Code Quagga</p>
      <div>
        <q-btn label="Iniciar Leitura" 
        color="primary"
        icon="mdi-barcode-scan"
        @click="initReader"
        >
          

        </q-btn>
      </div>
      <div id="reader"> </div>
    </q-page>

  </q-page>
</template>

<script>
import { defineComponent } from 'vue'
import Quagga from 'quagga'; // ES6

export default defineComponent({
  name: 'IndexPage',
  setup() {
    const initReader = () => {
      Quagga.init({
        inputStream: {
          name: "Live",
          type: "LiveStream",
          target: document.querySelector('#reader')    // Or '#yourElement' (optional)
        },
        decoder: {
          readers: ["ean_reader"]
        }
      }, function (err) {
        if (err) {
          console.log(err);
          return
        }
        console.log("Initialization finished. Ready to start")
        Quagga.start()
        Quagga.onDetected(() => {
          console.log('Detectado')
        })
      })
    }

    const stopReader = () => {
      Quagga.stop()
    }

    // const onDetected = (data) =>{
    //   console.log(data)
    // }
    return {
      initReader,
      stopReader
    }
  }
})
</script>
