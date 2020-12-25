<template>
    <div class="question" v-bind:class=" (isAnsRight ? 'right' : 'incorrect') ">
        <p>
            <slot></slot>
        </p>
        <div class = "variants">
            <label v-for="(text, key) in variants" v-bind:key="key">
                <input type="checkbox" v-model="checkboxes" v-bind:value="key"> {{key}}
            </label>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Question',
        props: ['variants'],
        data(){
            return{
                checkboxes: []

            }
        },
        computed: {
            isAnsRight(){
                let rightVars=[];
                for(let key in this.variants){
                    if(this.variants[key] == true)
                        rightVars.push(key)
                }
                let isAllRightChecked =true;

                for(let el of rightVars){
                    if(this.checkboxes.indexOf(el)== -1)
                        isAllRightChecked = false;
                }

                let isNoIncorrect = true;
                for(let el of this.checkboxes){
                    if(this.variants[el]==false)
                        isNoIncorrect=false;
                }

                return isAllRightChecked && isNoIncorrect

            }
        }

    }
</script>

<style>
    .question{
        width: 500px;
        padding: 20px;
        border: #333 solid;
        border-radius: 5px;
    }
    .right{
        background-color: #4fa30e;
    }
    .incorrect{
        background-color: red;
    }
</style>