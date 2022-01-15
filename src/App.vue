<template>
  <div class="container-app">
    <div class="container-quiz">  
      <div class="quiz-header">
          <h1 >Me conoces?</h1>
      </div>
        <div class="step-progress" :style="{'width': progress + '%'}"></div>

      <div class="quiz-main" v-for="(element,index) in questions.slice(a,b)" :key="index" v-show="quiz">
        <div class="box-question">
         <h2>Pregunta {{b}}/{{questions.length}}</h2>
          <p>{{element.question}}</p>
        </div>
        <div class="box-suggestions">
            <ul>
              <li v-for="(item,index) in element.suggestions" :key="index" :class="select ? check(item) : '' " @click="selectResponse(item)">
                    {{item.suggestion}}
                    <div class="fas fa-check" v-if="select ? item.correct: '' "></div>
                    <div class="fas fa-times" v-if="select ? !item.correct: '' "></div>
              </li>
            </ul>
        </div>
      </div>
      <div class="box-score" v-if="score_show">
          <h2>Tu puntuación es:</h2>
          <h2>{{score}}/{{questions.length}}</h2>
          <div class="btn-restart">
                <button @click="restartQuiz">Restart <i class="fas fa-sync-alt"></i></button>
          </div>
      </div>
    <div class="quiz-footer">
        <div class="box-button" v-if="progress < 100">
          <button  @click="skipQuestion" :style="!next ? 'background-color: rgb(106,128,202)' : '' ">Skip</button>
          <button  @click="nextQuestion" :style="next ? 'background-color: rgb(106,128,202)' : '' ">Siguiente</button>
        </div>
    </div>
  
  </div>
</div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return{ 
      questions:[
        {
          question: '¿Cuántos años tengo?',
          suggestions:[
            {suggestion:'18'},
            {suggestion:'24',correct:true},
            {suggestion:'28'},
            {suggestion:'21'}
          ]
        },
        {
          question: '¿Juego favorito?',
          suggestions:[
            {suggestion:'Fortnite'},
            {suggestion:'Left 4 dead 2', correct:true},
            {suggestion:'League of Legends'},
            {suggestion:'Dota 2'}
          ]
        },
        {
          question: '¿Intereses?',
          suggestions:[
            {suggestion:'Fiestas'},
            {suggestion:'Pasear'},
            {suggestion:'Gaming',correct:true},
            {suggestion:'Ver tv'}
          ]
        },
        {
          question: '¿Animal favorito?',
          suggestions:[
            {suggestion:'Gatos',correct:true},
            {suggestion:'Conejos'},
            {suggestion:'Perros'},
            {suggestion:'Peces'}
          ]
        },
        {
          question: '¿Carrera?',
          suggestions:[
            {suggestion:'Soporte'},
            {suggestion:'Desarrollador',correct:true},
            {suggestion:'Redes'},
            {suggestion:'Seguridad e Informatica'}
          ]
        },
        {
          question: 'Modelo de Telefono',
          suggestions:[
            {suggestion:'Samsung A11'},
            {suggestion:'Samsung Galaxy S7',correct:true},
            {suggestion:'iPhone X'},
            {suggestion:'Redmi Note Pro'}
          ]
        },{
          question: 'Como se llama mi novia :v',
          suggestions:[
            {suggestion:'Fiorella',correct:true},
            {suggestion:'Luana',correct:true},
            {suggestion:'Kelly',correct:true},
            {suggestion:'Sayuri',correct:true}
          ]
        }
      ],
      a:0,
      b:1,
      select:false,
      score:0,
      quiz:true,
      score_show:false,
      next: false,
      progress: 0,
    }
  },
  methods:{
    selectResponse(e){

        this.select = true;
        this.next = true;
        if(e.correct){
            this.score++;
        }  
    },
    check(status){
        if(status.correct){
            return 'correct'
        }else{
          return 'incorrect'
        }
    }, nextQuestion(){
      
      if(!this.next){

          return;
        }

      this.progress = this.progress + (100/this.questions.length);

      if(this.questions.length -1 == this.a){
        this.score_show = true;
        this.quiz = false;
      }else{
      this.a++;
      this.b++;
      this.select = false;
      this.next = false;
      }

      
  }, skipQuestion(){

    if(this.next){

          return;
        }

      this.progress = this.progress + (100/this.questions.length);

    if(this.questions.length - 1 == this.a){
        this.score_show = true;
        this.quiz = false;
  }else{
     this.a++;
     this.b++;

  }
  }, restartQuiz(){
    Object.assign(this.$data, this.$options.data()); 
  }
  }
}
</script>
