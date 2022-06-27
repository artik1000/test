<template>
    <form action="#" method="post" id="filter" onsubmit="return false" onload="beforeMount()">
        <div>
            <div class="sel">
                <div @click="ShowFirst()"><input type="text" v-model="maininput"/></div>
                <div
                        @click="reset()"
                >❌</div>
            </div>
            <div class="inp" v-if="first">
                <div class="sersel">
                    <div
                            @click="maininputall(elem)"
                        >Select all
                    </div>
                    <div>
                        <input v-model="searchvalue" class="search" placeholder="Search"/>
                    </div>
                </div>
                <ElementList
                        v-for="elem of SearchFun"
                        :key="elem.id"
                        @click="elem.selected = !elem.selected; elemminus(elem)"
                        v-bind:class="{active: elem.selected, active2: all}"
                        v-bind:elem="elem"
                />
                <div>
                    <input style="width: 100%" type="submit" value="Apply"/>
                </div>
            </div>
        </div>
        <div><input type="submit" v-on:click="getRequest()" value="send"/></div>
    </form>
</template>
<script>
import axios from 'axios'
import ElementList from '@/components/ElementList.vue'
export default {
    name: 'FormIn',
    components: {
        ElementList
    },
    data(){
        return{
            categories: [],
            errors: [],
            first: false,
            searchvalue: '',
            maininput:'',
            all: false
        }
    },
    methods: {
        ShowFirst() {
            this.first = !this.first;
        },
        reset (){
            this.maininput = ' ';
            this.first = !this.first;
        },
        maininputall() {
            var max = this.categories.length;
            for (var i = 0; i < max; i++) {
                this.maininput = this.maininput + ' ' + this.categories[i].name;
                this.all = true;
            }
        },
        elemminus (elem){
            console.log(elem.selected);
            if (elem.selected === false)
            {this.maininput = this.maininput.replace(elem.name,'')}
            if(elem.selected ===true){
            this.maininput = this.maininput + ' ' + elem.name;
            }

        }
    },
    computed: {
        SearchFun() {
            return this.categories.filter(item => item.name.indexOf(this.searchvalue) !== -1)
        },
    },
    beforeMount () {
            axios({
                method: 'get',
                url: ' http://localhost:3000/categories:',
                // url: 'https://lobster.tools/api/v1/categories',
                // url: 'https://lobster.tools/api/v1/projects',
                headers: {
                    "Content-type": "application/json; charset=UTF-8",
                    'Access-Control-Allow-Headers': 'x-requested-with, Content-Type, origin, authorization, accept, x-access-token',
                    'Access-Control-Allow-Origin': '*',
                    'Access-Control-Allow-Methods': 'POST, GET, OPTIONS, DELETE, PUT',
                    'Access-Control-Allow-Max-Age': '1000',
                    'Authorization': 'Bearer BT3HK2NpCnyrKiDo',//
                }
            })
                .then(response => {this.categories = response.data})
                .catch(function(error) {
                    console.log(error);
                });
    },
}
</script>
<style>
    .sel {
        display: flex;
        flex-direction: row;
        border: 1px solid;
        color: lightgray;
        border-radius: 2px;
    }
    .search{
        border: 1px solid !important;
    }
    .inp{
        display: flex;
        flex-direction: column;
    }
    .sersel{
        display: flex;
        flex-direction: row;
    }
    .active{
        background-color: red;
        color: white;
    }
    .active2{
        background-color: red;
        color: white;
    }
    form {
        display: flex;
        flex-direction: row;
    }
    input {
        -webkit-appearance: none;
        -moz-appearance: none;
        border: none;
        position: relative;
        outline: none;
        padding: 5px;
        padding-right: 40px;
    }

</style>