<template>
    <div class="app">
        <h1>Random GIF Cat</h1>
        <div class="row ">
            <form action="">

                <div class="input">
                    <label>Titulo: </label>
                    <input type="text" v-model="cat.title">
                </div>
                <div class="input">
                    <label>Filtro: </label>
                    <select @change="filterChange($event)">
                        <option value="">Seleccione Filtro</option>
                        <option value="sepia">Sepia</option>
                        <option value="mono">Mono</option>
                        <option value="blur">Blur</option>
                        <option value="pixel">Pixel</option>
                        <option value="negative">Negative</option>
                    </select>
                </div>
                <div class="input">
                    <label>Color: </label>
                    <select  id="" @change="colorChange($event)">
                        <option value="">Seleccione Color</option>
                        <option value="red" >rojo</option>
                        <option value="green" >verde</option>
                        <option value="white" >blanco</option>
                        <option value="blue" >azul</option>
                        <option value="yellow" >amarillo</option>
                    </select>
                </div>

                <div class="input">
                    <label>Tamaño: </label>
                    <input type="text" v-model="cat.size">
                </div>
            </form>

        </div>
        <button  @click="search">Obtener mi gato</button>

        <div>
            <span v-show="cat.isLoading"> Buscando gato... </span>
            <img v-show="!cat.isLoading" :src="cat.image"  >
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return { 
            
                cat: {
                    isLoading:false,
                    title:"",
                    filter:"",
                    color:"",
                    size:"",
                    image:"",
                    
                }

            }
        },
        methods: {
            search() {
            this.cat.isLoading = true
            fetch(`https://cataas.com/cat/gif/says/${this.cat.title}?filter=${this.cat.filter}&color=${this.cat.color}&size=${this.cat.size}`)
            .then(response => this.cat.image = response.url )
            .then(()=> this.cat.isLoading = false)
            },
            filterChange(event){
                this.cat.filter = event.target.value
            },
            colorChange(event){
                this.cat.color = event.target.value
            },
          

        },
        
        computed:{
         
        catTitle(){
          return this.cat.title;
        },
        catFilter(){
          return this.cat.filter;
        },
        catColor(){
          return this.cat.color;
        },
        catSize(){
            return this.cat.size;
        }


        }
    }
</script>

<style>
    html {
        background: lightblue;
        text-align: center;
    }

    h1 {
        text-align: center;
    }

    .row {
        text-align: center;
        background: lightcoral;
        padding: 0.7em;
    }

    .input {
        margin: 1em;
        padding: 0.3rem;
    }

     button {
        margin:2rem;
        border-radius :4px;
        border:none;
        padding:10px;
        background: rgb(255, 94, 94);
        color:#fff;
        font-size: 18px;
    }
    button:hover{
         background:  lightcoral;

    } 

    input,
    select {
        padding: 0.3rem;
        border-radius: 4px;
        border:none;
    }
</style>