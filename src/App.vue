<template>
  <div id="app">
    
    <div class="urna">
      <Tela
        :tela="tela"
        :numeroVoto="numeroVoto"
        :quantidadeNumeros="quantidadeNumeros"
        :candidato="candidato"
      />
      <Teclado
        :adicionarNumero="adicionarNumero"
        :corrigir="corrigir"
        :confirmar="confirmar"
        :votarEmBranco="votarEmBranco"
      />
    </div>
  
  </div>
</template>

<script>

import '@/css/global.css';

import Teclado from '@/components/Teclado';
import Tela from '@/components/Tela';
import confirmAudio from '@/assets/audios/confirm.wav';
import keyAudio from '@/assets/audios/key.wav';

export default {
  name: 'App',
  components: {
   Teclado,
   Tela
  },
  methods:{
    adicionarNumero(numero){

      this.executarSom(keyAudio);

      if(this.numeroVoto.length == this.quantidadeNumeros){
        return false;
      }

      this.numeroVoto += ''+numero;
      this.verificarCandidato();
    },
    verificarCandidato(){
      if(this.numeroVoto.length < this.quantidadeNumeros){
        return false;
      }

      if(this.candidatos[this.tela][this.numeroVoto]){
        this.candidato = this.candidatos[this.tela][this.numeroVoto];
        return true;
      }

      this.candidato = {
        nome: 'Voto nulo',
        partido: 'Voto nulo',
        imagem: ''

      }
    },
    corrigir(){
      this.executarSom(keyAudio);
      this.limpar();
    },
    limpar(){
      this.candidato = {}
      this.numeroVoto = ''
    },
    confirmar(){
      if(this.numeroVoto.length < this.quantidadeNumeros){
        return false;
      }

      return this.avancarTela();
    },
    avancarTela(){

      this.executarSom(confirmAudio);

      if(this.tela == 'prefeito'){
        this.tela = 'vereador';
        this.quantidadeNumeros = 5;
        return this.limpar();
      }

    this.tela = 'fim';

    var instancia = this;

    setTimeout(function(){
      instancia.tela = 'prefeito'
      instancia.quantidadeNumeros = 2
      return instancia.limpar();
    },3000);
  },

  votarEmBranco(){
    if(this.tela == 'fim') return false; 

    this.limpar();
    this.avancarTela();
  },
  executarSom(arquivoSom){
    if(arquivoSom){
      let audio = new Audio(arquivoSom);
      audio.play();
    }
  }

  },
  data(){
    return{
      tela: 'prefeito',
      numeroVoto: '',
      quantidadeNumeros: 2,
      candidato:{},
      candidatos: {
          "prefeito":{
            "01":{
              "nome": "Kadu",
              "partido": "Técnologia Batman",
              "imagem": "https://cdn.discordapp.com/attachments/756687351668932689/918917749114286171/Kadu.jpeg"
            },
            "04":{
              "nome": "Khayo",
              "partido": "Supreme",
              "imagem": "https://cdn.discordapp.com/attachments/756687351668932689/918917749659566150/Khayo.jpeg"
            },
            "13":{
              "nome": "Kharem",
              "partido": "Ula-Ula",
              "imagem": "https://cdn.discordapp.com/attachments/756687351668932689/918917748711653407/Kharem.jpeg"
            },
            "32":{
              "nome": "JOJO",
              "partido": "Wooooo",
              "imagem": "https://giffiles.alphacoders.com/162/162110.gif"
            },
            "10":{
              "nome": "Gatineo",
              "partido": "Miau",
              "imagem": "https://pbs.twimg.com/profile_images/427933217589436416/4D9WknWg_400x400.jpeg"
            },
            "25":{
              "nome": "Bob Esponja",
              "partido": "Fenda do Biquíni",
              "imagem": "https://i.gifer.com/origin/43/43d799f7d93fc9eb83522b56a87bb97c.gif"
            },
            "08":{
              "nome": "Vegeta",
              "partido": "Dragon Ball",
              "imagem": "https://raw.githubusercontent.com/william-costa/wdev-urna-eletronica-resources/master/images/vegeta.png"
            },
            "06":{
              "nome": "Rogers",
              "partido": "Oh no!!!",
              "imagem": "https://img.r7.com/images/fotos-comprovam-que-cachorros-sao-os-pets-mais-engracados-20032018161340130?dimensions=650x650"
            },
            "14":{
              "nome": "Busanfa",
              "partido": "Fashion",
              "imagem": "https://cdn.discordapp.com/attachments/756687351668932689/918917157214113862/3.jpg"
            }
          },
          "vereador":{
            "01234":{
              "nome": "O Empresário",
              "partido": "Dog show",
              "imagem": "https://i.pinimg.com/originals/e6/a4/e6/e6a4e662cbb15022326cc77bf21d98ea.jpg"
            },
            "00002":{
              "nome": "Pards",
              "partido": "O brabo",
              "imagem": "https://c.tenor.com/HfYaPgo1dqAAAAAd/cachorro-assustado.gif"
            },
            "00150":{
              "nome": "Miauzin",
              "partido": "Just Dance",
              "imagem": "https://static.imgs.app/content/assetz/uploads/2018/08/gif-frase-para-animados-engracados-4-011.gif"
            },
            "08001":{
              "nome": "Pards",
              "partido": "Cavalaria 2.0",
              "imagem": "http://s2.glbimg.com/Mu4cJYfYsrt1jIlZQMm3dzOC-UKqTZzwTxP3sw9f0dFIoz-HdGixxa_8qOZvMp3w/s.glbimg.com/jo/g1/f/original/2013/03/11/cavalozuao1.jpg"
            },
            "12020":{
              "nome": "Ozmá",
              "partido": "Ku klux klã",
              "imagem": "https://animais.culturamix.com/blog/wp-content/gallery/os-15-animais-mais-engracados-da-internet-5/Os-15-Animais-Mais-Engracados-da-Internet-13.jpg"
            },
            "10001":{
              "nome": "Petterson",
              "partido": "Dogs do bem",
              "imagem": "https://img.r7.com/images/fotos-comprovam-que-cachorros-sao-os-pets-mais-engracados-20032018161341172?dimensions=650x705"
            },
            "12003":{
              "nome": "Jonas",
              "partido": "do beco",
              "imagem": "https://i.redd.it/bznsluowgvk31.jpg"
            }
          }
        } 
    }
  }
}
</script>

<style>
#app {
  background-color: var(--background-color);
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center; /** Horizontal */
  align-items: center; /** Vertical */
}

.urna {
  width: 1000px;
  height: 500px;
  background-color: var(--ballot-box-background-color);
  padding: 30px;
  border-radius: 5px;
  display: flex;
  justify-content: space-between;
}
</style>
