<template>
    <div class="question" v-bind:class=" (isAnsRight ? 'right' : 'incorrect') ">
        <p>
            <slot></slot>
        </p>
        <div class = "variants">
            <label v-for="(text, key) in variants" v-bind:key="key">
                <input type="checkbox" v-model="chexboxes" v-bind:value="key"> {{key}}
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
                chexboxes: []

            }
        },
        computed: {
            isAnsRight(){
                let rightVars=[];
                for(let key in this.variants){
                    if(this.variants[key] == true)
                        rigthVars.push(key)
                }
                let isAllRightChecked =true;

                for(let el of rightVars){
                    if(this.chexboxes.indexOf(el)== -1)
                        isAllRightChecked = false;
                }

                let isNoIncorrect = true;
                for(let el of this.variants){
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
    .incorrecct{
        background-color: red;
    }
</style>