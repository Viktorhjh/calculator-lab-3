<template>
  <div :class="wrapper">
    
    <div>
        <input v-model="current" id="res">
    </div>
    <button @click="reset()" :class='bigButtons' v-if="bool" type="reset">C</button>
    <button @click="resetSymbol()" :class='bigButtons' v-else type="reset">&larr;</button>
    <template v-for = "i in contents" :key="i.id">
        <button @click="addNumber(i.content)" :class="button" > {{i.content}} </button>
    </template>
    <button @click="res()" :class='bigButtons'>=</button>

  </div>  
</template>

<script>
let id = 0;
export default{
    data(){
        return{
            button: 'buttons',
            bigButtons: 'bigButton',
            wrapper: '',         
            bool: true,            
            
            current: '',
            contents: [
                {id:id++, content:'.'},
                {id:id++, content:'/'},
                {id:id++, content:'7'},
                {id:id++, content:'8'},
                {id:id++, content:'9'},
                {id:id++, content:'*'},
                {id:id++, content:'4'},
                {id:id++, content:'5'},
                {id:id++, content:'6'},
                {id:id++, content:'-'},
                {id:id++, content:'1'},
                {id:id++, content:'2'},
                {id:id++, content:'3'},
                {id:id++, content:'+'},  
                {id:id++, content:'+-'},                
                {id:id++, content:'0'}
            ]
        }
    },
    methods: {
      reset() {
      this.current = '';
      this.bool = true;
    },     
    addNumber(n) {                
      this.current += n;
      this.bool = false;
    },
    resetSymbol() {
      this.current = this.current.substr(-this.current.length, this.current.length-1);
    },
    res() {
        this.bool = true;
        let s = this.current.split(/[-\*\+\/]/);             
        let op = '';     
        let res;   

        if(this.current.includes('+'))
            op = '+';

        if(this.current.includes('-'))
            op = '-';
            
        if(this.current.includes('*'))
            op = '*';

        if(this.current.includes('/'))
            op = '/';

        switch(op){
            case '+':
                res = parseFloat(s[0]) + parseFloat(s[1]);
                break;

            case '-':
                res = parseFloat(s[0]) - parseFloat(s[1]);
                break;
                
            case '*':
                res = parseFloat(s[0]) * parseFloat(s[1]);
                break;
                
            case '/':
                res = parseFloat(s[0]) / parseFloat(s[1]);
                break;
            }
            this.current = res;
        }
        
  }
}
</script>

<style scoped>   

    button{
    background: none;
    border-width: 1px;		
    border: none;
    background: #B7C8D1;
    font-size: 200%;
    padding: 10px;
    margin: 10px;
    height: 60px;
    width: 60px;
    }

    .bigButton{
    height: 60px;
    width: 140px;	
    }

    input{	
    background: #D5E8F2;
    width: 300px;
    font-size: 200%;
    padding: 10px;
    margin: 10px;
    border-width: 1px;	
    }

    button:hover{
    background: #9FADB5;
    }

</style>
