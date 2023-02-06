<template>
    <div class="box">
        <b-jumbotron >
            <p>{{question}}</p>
            <h1>{{i++}}</h1>
            <hr>
        <b-list-group>
            <b-list-group-item 



            v-for="(answer,index) in all" 
            :key="index"
            
            @click="activate(index)" 
            :class="
            
            [
          
            
            answered &&    correct_index === index ? 'correctAnswer' :
            answered && selected == index &&   correct_index !== index  ? 'incorrectAnswer' : ''
            
            
            ,
            
            ,{activeAnswer : active_el == index}
            ,{disabled : disable}
            
            ]" 


            >
            
            
            {{answer}}
            
            
            </b-list-group-item>


        </b-list-group>
             <b-button variant="primary" class="mr-4 mt-5"
             @click="submit"
             :disabled="submitDisable"
             >Submit</b-button>
             <b-button variant="success" class="mt-5" 
             
             @click="next"

          
             
             >{{btnText}}</b-button>
        </b-jumbotron>   
    </div>
</template>

<script>
import  _ from 'lodash'
export default {
    name:'QuestionBox',
    data(){
        return{
            i:0,
            sayed:null,
            selected:false,
            cindex:0,
            active_el:-1,
            answered:false,
            correct_index:null,
            disable:false,
            submitDisable:true,
            btnText:"Next"
        }
    },
    props:{
       question:String,
       indexQ:Number,
       incorrect_answers:Array,
       correct_answer:String,
       increment:Function,
       correct:Number,
       total:Number
    },
    methods:{
       

       submit(){
            
              this.correct_index = this.all.indexOf(this.correct_answer)
          
            console.log(this.selected)
            this.answered = true
            this.increment(this.correct_index == this.selected)
            this.disable = true
            this.submitDisable = true  
        
              
       },
        next(){
         
            if(this.cindex == 8){
                this.btnText = "Done !"
                
                alert(`Congratzzz!! exam ended you solved `+ this.correct +` out of `+ this.total)
                
                  return 1
            }
               
           
            
            this.active_el = -1
            this.correct_index = -1
            this.disable = false
            this.selected = false
            this.answered = false
            this.$emit('update:indexQ',++this.cindex)
           
        },
        activate(el){
         
            this.active_el = el
            this.selected = el
            this.submitDisable= false
           
        }
        
    },
    computed:{
        all(){
            let arra1  = [...this.incorrect_answers]
            arra1.push(this.correct_answer)
            arra1 = _.shuffle(arra1)
            return arra1
     }
 }
} 
</script>

<style scoped>
    .box{
        margin:  auto;
       width: 40%;



    }.list-group-item:hover{
        background: lightgray;
         cursor: pointer;
    }.activeAnswer{
        background: rgb(145, 143, 143) !important;
        color: white !important;;
    }.correctAnswer{
        background: rgb(82 208 56) !important;
         color: white  !important;;
    }.incorrectAnswer{
        background: #c15858 !important;
         color: white !important;;
    }
    
   
</style>