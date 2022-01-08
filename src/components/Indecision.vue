<template>
 
        <!-- <h1 class="titulo">INDECISION 🤔</h1> -->

        <img v-if="img" :src="img" alt="bg">
        <div class="bg-dark">

        </div>
        <div class="indecision-container">

            <input v-model="question" type="text" placeholder="Hazme una pregunta">
            <p class="question" >Recuerda terminar con un signo de interrogación (❓)</p>
            <div v-if="isValidQuestion">
                <h2 > {{  question }}</h2>
                <h1>  {{ answer === 'yes' ? 'Si!' : 'No!' }}</h1>
            </div>
        </div>
  
</template>

<script>
export default {
   name: 'Indecision',

   data() {
       return {
           question : '',
           answer: 'Thinking...🤔',
           img : null,
           isValidQuestion : false
       }
   },
   watch: {
       question( value, oldValue){
        //    console.log( value.includes('?') )
             this.isValidQuestion = false
           if (!value.includes('?')) {
               return 
              // console.log('No Contine ?')
           }else{
            // Llamada a http
                this.isValidQuestion = true,
                this.getAnswer()

           }
           
       }
   },
   methods: {
     async  getAnswer(){
           this.answer = 'Thinking...🤔'
           /* desestructuro lo que me viene en la respuesta */
           const { answer, image } = await fetch('https://yesno.wtf/api')
                .then(res => res.json())
                console.log(answer, image)

                this.answer = answer 
                this.img = image            

    }
   },
}

</script>




<style scoped>

    img, .bg-dark {
        height: 100vh;
        left: 0px;
        max-height: 100%;
        max-width: 100%;
        position: fixed;
        top: 0px;
        width: 100vw;
    }

    .bg-dark {
        background-color: rgba(0, 0, 0, 0.4);
    }

    .indecision-container {
        position: relative;
        z-index: 99;
    }
    
    input {
        width: 250px;
        padding: 10px 15px;
        border-radius: 5px;
        border: none;
        margin-top: 150px;
    }
    input:focus {
        outline: none;
    }

    p {
        color: white;
        font-size: 20px;
        margin-top: 20px;
    }

    h1, h2 {
        color: white;
    }
    
    h2 {
        margin-top: 150px;
    }
    h1.titulo{
         color: rgb(20, 19, 19);
    }

</style>